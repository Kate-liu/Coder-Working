# Disruptor之性能分析

## 前言

> 本文属于Disruptor这个java领域中高性能队列的第三篇文章，希望回看前面两篇：
>
> [Disruptor之高速缓存行设计](https://www.copydays.org/2020/06/11/disruptor之高速缓存行设计/)，[Disruptor之无锁实现](https://www.copydays.org/2020/06/12/disruptor之无锁实现/)。
>
> 本文会主要聚焦于全局梳理Disruptor，并且一起探讨性能这个瓶颈，回看一下局部性原理，并且接触一下并发编程中的名词：“伪共享”。

注意：三篇文章也只是介绍了一些关于Disruptor的关键点，剩下的还需要自己在实践中领悟。



## 正文

>本文需要具备的基础知识：知道局部性原理，知道CPU 高速缓存，知道java常见有界队列，有并发编程经验，等。（本文是一个综合的汇合，详细内容是一提而过，但会给出链接。）
>

### 一、回看Disruptor

由于Disruptor是应用于java领域的，所以将其和SDK中的有界队列（ArrayBlockingQueue，LinkedBlockingQueue）对比，在[Disruptor之无锁实现](https://www.copydays.org/2020/06/12/disruptor之无锁实现/#Disruptor之无锁实现)文中提到过。

其应用领域非常广泛，如：Log4j，Spring Messaging，HBase，Storm等。

**官网介绍Disruptor的一句话：A High Performance Inter-Thread Messaging Library。**

Disruptor的性能高的原因是其精巧的设计，尤其是无锁操作。ArrayBlockingQueue，LinkedBlockingQueue都是基于ReentrantLock实现，如下所示：

```java
// ArrayBlockingQueue
	/** Main lock guarding all access */
    final ReentrantLock lock;

// LinkedBlockingQueue
    /** Lock held by put, offer, etc */
    private final ReentrantLock putLock = new ReentrantLock();
```





### 二、Disruptor论文

注意：编程不只是一个实践的操作，很多设计与实践，都是有论文支撑的，所以有必然了解一下，那些严谨的学术理论。

关于Disruptor的论文，主要将其性能描述为：

**1.Disruptor的内润分配更加合理，使用RingBuffer这种数据结构，将数组元素在初始化的时候，一次性全部创建，提升缓存命中率，对象循环利用，避免频繁的GC。**

**2.可以避免伪共享，提升缓存利用率。**

**3.采用无锁算法，避免频繁加锁，解锁的性能消耗。**

**4.支持批量消费操作，消费者可以无锁方式消费多个消息（Event）。**





### 三、Disruptor使用

注意：学习一个技术和框架的时候，最直接，最快的方式就是直接上官网，不要惧怕英文，多看就看的快了。

从这里开始[Getting the Disruptor](#https://github.com/LMAX-Exchange/disruptor/wiki/Getting-Started#getting-the-disruptor)，可以将官方示例总结为：

#### 1）Event

**在Disruptor中，生产者生产的对象和消费者消费的对象叫做Event，使用Disruptor的时候，需要自定义Event，如：**

```java
public class LongEvent
{
    private long value;

    public void set(long value)
    {
        this.value = value;
    }
}
```



#### 2）构建Disruptor对象

**构建Disruptor对象除了要指定队列大小外，还需要传入一个EventFactory。**



#### 3）消费Event

**消费Disruptor中Event的似乎，需要通过handleEventsWith()，方法注册一个事件处理器，发布Event则需要通过publishEvent()方法。**

关于java8中Disruptor的示例代码，如下所示：

```java
import com.lmax.disruptor.dsl.Disruptor;
import com.lmax.disruptor.RingBuffer;
import com.lmax.disruptor.util.DaemonThreadFactory;
import java.nio.ByteBuffer;

public class LongEventMain
{
    public static void main(String[] args) throws Exception
    {
        // Specify the size of the ring buffer, must be power of 2.
        int bufferSize = 1024;

        // Construct the Disruptor
        Disruptor<LongEvent> disruptor = new Disruptor<>(LongEvent::new, bufferSize, DaemonThreadFactory.INSTANCE);

        // Connect the handler
        disruptor.handleEventsWith((event, sequence, endOfBatch) -> System.out.println("Event: " + event));

        // Start the Disruptor, starts all threads running
        disruptor.start();

        // Get the ring buffer from the Disruptor to be used for publishing.
        RingBuffer<LongEvent> ringBuffer = disruptor.getRingBuffer();

        ByteBuffer bb = ByteBuffer.allocate(8);
        for (long l = 0; true; l++)
        {
            bb.putLong(0, l);
            ringBuffer.publishEvent((event, sequence, buffer) -> event.set(buffer.getLong(0)), bb);
            Thread.sleep(1000);
        }
    }
}
```





### 四、再谈RingBuffer

#### 1）ArrayBlockingQueue

ArrayBlockingQueue，从名字就可以看出来是使用**数组**作为底层存储队列。

源码如下所示：

```java
    /** The queued items */
    final Object[] items;
```

在ArrayBlockingQueue中添加一个元素，需要先创建一个元素，然后将元素的地址存储在数组的某个索引位置，由于创建时间是不连续的，那么在内存中的位置，一定是不连续的，对应的数据缓存命中基本为0.

![ArrayBlockingQueueAddElement](57-Disruptor之性能分析.assets/ArrayBlockingQueueAddElement.png)





#### 2）Disruptor

Disruptor使用的底层存储结构是RingBuffer，本质也是使用数组。

在[局部性原理](https://www.copydays.org/2020/05/22/局部性原理/)中，介绍过**时间与空间局部性，对应于Disruptor的缓存行填充和数组存储结构。**

所以，Disruptor会一开始就将所有的对象全部初始化创建好，所以内存中的数据会是连续的，那么数据一定会命中缓存。

对应的源码如下：

```java
    // availableBuffer tracks the state of each ringbuffer slot
    // see below for more details on the approach
    private final int[] availableBuffer;
    private final int indexMask;
    private final int indexShift;

    /**
     * Construct a Sequencer with the selected wait strategy and buffer size.
     *
     * @param bufferSize   the size of the buffer that this will sequence over.
     * @param waitStrategy for those waiting on sequences.
     */
    public MultiProducerSequencer(int bufferSize, final WaitStrategy waitStrategy)
    {
        super(bufferSize, waitStrategy);
        availableBuffer = new int[bufferSize];
        indexMask = bufferSize - 1;
        indexShift = Util.log2(bufferSize);
        initialiseAvailableBuffer();
    }
```

Disruptor中的RingBuffer的存储结构使用数组的形式，将一个一个Event全部初始化存储在数组中，当需要发布一个Event的时候，并不是创建一个新的Event，而是将内部的Event循环利用，调用 event.set()方法，需要内容。这就避免了频繁的GC。

![Disruptor 内部 RingBuffer 结构图](57-Disruptor之性能分析.assets/Disruptor 内部 RingBuffer 结构图.png)





### 五、理解伪共享

伪共享属于CPU高速缓存中的一个名词。

简言之，将其解释为：多个数据加载不同CPU核心之后，由于数据修改导致其他核心中的缓存行数据失效。

想要深入的了解缓存行的失效，阅读[缓存一致性之MESI协议](https://www.copydays.org/2020/05/25/缓存一致性之mesi协议/#缓存一致性之MESI协议)。

在CPU中，现在一般加载的缓存行是64字节，也就是64Bytes，但是一个数据不会刚好64Bytes，那么剩下的位置，会加载与其内存中连续的数据，此时满足空间局部性原理，如果命中缓存就可以提升性能。

但是，如果另一个CPU核心，也同时加载了这个缓存行的另一个变量数据，那么一旦另一个核心修改了变量，本核心的缓存行就直接失效了，注意：失效单位是缓存行，不是变量失效。

那么，此时CPU核心就需要强制加载内存中的数据，此时的性能，就慢太多了。从[计算机存储器的层次结构简介](https://www.copydays.org/2020/05/21/173/)中，可以知道CPU访问高速缓存的时间是远远快于访问内存的。

所以，伪共享指的是由于共享缓存行导致缓存失效的场景，看看下图描述。

![CPU 缓存示意图](57-Disruptor之性能分析.assets/CPU 缓存示意图.png)

一旦有一个变量数据更改之后，所有的缓存行数据其实都是失效的，那么就会变成下图。

![CPU 缓存失效示意图](57-Disruptor之性能分析.assets/CPU 缓存失效示意图.png)

为了解决伪共享，也就是保证每个白能量独占一个缓存行，不共享缓存行，具体技术就是缓存行填充。







### 六、再谈CAS之无锁实现

如果你看了[Disruptor之无锁实现](https://www.copydays.org/2020/06/12/disruptor之无锁实现/)，你就会知道其实无锁只是利用了CPU提供的原子指令cmpchg。

反之，如果不适用指令，为了保证数据的竞争，就需要加锁实现，保证数据进入队列和出队列的时候只有一个线程操作，那么这个性能就会大打折扣。

基于Disruptor的实现，队列的入队，需要保证不能覆盖没有消费的元素，对于出队操作，需要保证不能读取没有写入的元素。所以，RingBuffer内部维护了入队索引，但是由于Disruptor的论文表示可以多个消费者同时消费，也就是没有出队索引，此时的出队索引就是所有消费线程中索引最小的一个。

关于Disruptor的入队操作核心代码如下所示，简单描述为：如果没有足够的空域位置，就出让CPU使用权，重新计算，反之则设置入队索引。

```java
// 生产者获取 n 个写入位置
do {
  //cursor 类似于入队索引，指的是上次生产到这里
  current = cursor.get();
  // 目标是在生产 n 个
  next = current + n;
  // 减掉一个循环
  long wrapPoint = next - bufferSize;
  // 获取上一次的最小消费位置
  long cachedGatingSequence = gatingSequenceCache.get();
  // 没有足够的空余位置
  if (wrapPoint>cachedGatingSequence || cachedGatingSequence>current){
    // 重新计算所有消费者里面的最小值位置
    long gatingSequence = Util.getMinimumSequence(gatingSequences, current);
    // 仍然没有足够的空余位置，出让 CPU 使用权，重新执行下一循环
    if (wrapPoint > gatingSequence){
      LockSupport.parkNanos(1);
      continue;
    }
    // 从新设置上一次的最小消费位置
    gatingSequenceCache.set(gatingSequence);
      
  } else if (cursor.compareAndSet(current, next)){  // CAS 操作
    // 获取写入位置成功，跳出循环
    break;
  }
} while (true);
```







## 结束语

关于Disruptor的内容，已经全部结束了！

如果没有带着问题来学习，时间一长就会忘记，所以看到这里的，哪怕很多东西不懂也没关系，毕竟学着学着就悟到了！

日拱一卒，不着急，不停歇！多想，多做！加油吧！







## 参考链接

1.Disruptor：https://github.com/LMAX-Exchange/disruptor/wiki/Introduction

2.Implementing Lock-Free Queues：http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.53.8674&rep=rep1&type=pdf

3.并发编程网：http://ifeve.com

