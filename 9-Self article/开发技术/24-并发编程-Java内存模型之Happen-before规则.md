# 并发编程|Java内存模型之Happen-before规则

## 前言

我会在接下来的2-3个月的时候，尝试从全局的角度建立**并发编程的全景图**。

这其中会涉及相关知识：**冯诺依曼体系架构，CPU，内存，I/O，网络，操作系统，Java**等。

在这一系列的文章中，我会尽可能写明白：**它是什么？他为什么是这样？**

用一句话总结一下并发编程：**并发编程为了解决性能问题，也解决了提升性能带来的新问题。**（有点绕？读三遍就好了！）





## 正文

本文将深度解读**Happen-before规则**，从这个角度看**并发的可见性和有序性**。

前文回顾：并发的可见性问题取决于**CPU的缓存机制**，并发的顺序性问题取决于**编译器的优化**。

一定要深刻的理解可见性和顺序性**本质的问题**，这样才可以看到就想到，也就算是学会了！

你还需要知道**Java内存模型是什么？**

**Java的内存模型，简称为JMM(Java memory model)，其规范了JVM如何提供按需禁用缓存和编译优化的方法。**

其次，你还需要知道**Happen-before真正表达的是前面的一个操作结果对后续操作是可见的。**

好了，有这两点的铺垫，可以开始Happen-before规则的了解了。

PS：本文示例代码较多，可以尝试打开idea，自己尝试**跑一遍**。





### 规则一：程序的顺序性规则

其，描述的是：**在一个线程中，程序是按照顺序执行的，前面的操作Happen-before于后续的任意操作。**

下面的示例代码中，最终的输出结果是**56**，也就表明了程序前面对某个变量的修改一定是对后续操作是可见的。

```java
package HappenBefore;

public class OrderClass {
    int index = 1;

    volatile boolean value = false;

    public void writer() {
        index = 56;
        value = true;
    }

    public void reader() {
        if (value) {
            System.out.println(index);
        }
    }

    public static void main(String[] args) {
        System.out.println("Start program.....");
        OrderClass orderClass = new OrderClass();
        orderClass.writer();  // 先执行index赋值操作，变为56
        orderClass.reader();  // 再执行读取操作，打印index的值，最后输出为56
        System.out.println("End program.....");
    }
}
```





### 规则二：volatile变量规则

其，描述的是：**对一个volatile变量的写操作，Happen-before之后对于这个volatile变量的读操作。**

示例代码如下所示，其中volatile的变量值value的写值，对于value的读值是可见的。

```java
package HappenBefore;

public class VolatileClass {
    int index = 1;

    volatile boolean value = false;

    public void writer() {
        index = 56;
        value = true;  // value的写值 Happen-before 读变量value
    }

    public void reader() {
        if (value) {
            System.out.println(index);
        }
    }

    public static void main(String[] args) throws Exception {
        System.out.println("Start program.....");
        VolatileClass volatileClass = new VolatileClass();
        // 创建两个线程
        Thread thread1 = new Thread(volatileClass::writer);
        Thread thread2 = new Thread(volatileClass::reader);
        // 启动线程
        thread1.start();
        thread2.start();
        // 等待线程结束
        thread1.join();
        thread2.join();
        System.out.println("End program.....");
    }
}
```



### 规则三：传递性

其，表述的意思是：**如果A操作Happen-before于B操作，B操作Happen-before于C操作，那么A操作Happen-before与C操作。**

示例代码，看规则二中代码。

其中，写index的操作 Happen-before于 写value的操作，写value的操作 Happen-before于 读value的操作，那么写index的操作 Happen-before于 读value操作。

此时，**线程thread1设置的index= 56，对于线程thread2是可见的。**





### 规则四：管程中锁的规则

其，表述的意思是：**对于一个锁的解锁 Happen-before 于后续对这个锁的加锁。**

**管程**，指的是一种通用的**同步原语**，在Java中指的是**synchronized**，synchronized是Java对管程的实现。并且synchronized在Java中是**隐式实现**的，也就是**加解锁是编译器实现**的，不需要手动实现。

示例代码如下所示，其中加解锁是**自动实现**的。

```java
package HappenBefore;

public class SyncClass {

    private long index = 4;

    private long countFunc() {  // 自动加锁
        synchronized (this) {
            if (this.index < 6) {
                this.index = 6;
            }
        }
        return index;
    }  // 自动解锁

    public static void main(String[] args) {
        SyncClass syncClass = new SyncClass();
        long result = syncClass.countFunc();
        System.out.println("The result is " + result);
    }
}
```





### 规则五：线程start() 规则

其，表述的意思是：**线程A启动子线程B之后，子线程B能够看到主线程在启动线程B之前的操作。**

示例代码如下，其中子线程thread可以看到主线程对于index值的修改。

```java
package HappenBefore;

public class StartClass {

    private static long index = 0;

    public static void main(String[] args) {
        // 创建线程
        Thread thread = new Thread(() -> {
            System.out.println("thread forward index value is " + index);
            index = 6;
            System.out.println("thread tail index value is " + index);
        });

        // 对index进行修改
        System.out.println("forward index value is " + index);
        index = 8;
        System.out.println("tail index value is " + index);
        
        // 启动线程
        thread.start();
    }
}

/*
output context：
    forward index value is 0
    tail index value is 8
    thread forward index value is 8
    thread tail index value is 6
 */
```







### 规则六：线程join() 规则

其，表述的意思是：**主线程A等待子线程B完成，当子线程B完成之后，可以看到子线程的操作。**

示例代码如下，最后的输出结果是“end index value is 666”，此时子线程对于index值的修改起作用了。

```java
public class JoinClass {
    private static long index = 2;

    public static void main(String[] args) throws Exception {
        // 创建线程
        Thread thread = new Thread(() -> {
            index = 666;
        });

        // 启动线程
        thread.start();

        // 等待线程结束
        thread.join();
        System.out.println("end index value is " + index);
    }
}

```









### 规则七：线程中断规则

其，表述的意思是：**对线程interrupt()方法的调用先行发生于被中断线程的代码检测到中断事件的发生。**

示例代码如下，其中通过Thread.interrupted()方法检测到是否有中断发生，使用interrupt() 主动触发一个中断。最后的结果为**true**。

```java
package HappenBefore;

public class InterruptedClass {
    private static long age = 18;

    public static void main(String[] args) throws Exception {
        // 创建线程
        Thread thread = new Thread(() -> {
            age = 23;
        });

        // 执行线程
        thread.start();
        thread.interrupt();  // Interrupting a thread

        boolean isInterrupted = thread.isInterrupted();
        System.out.println("isInterrupted " + isInterrupted);
    }
    
}
```





### 规则八：对象终结规则

其，表述的意思是：**一个对象的初始化完成(构造函数执行结束)先行发生于它的finalize()方法的开始。**

这个规则很简单，属于类的初始化相关内容。这里奉对象的**finalize方法源码**。

```java
 /**
     * Called by the garbage collector on an object when garbage collection
     * determines that there are no more references to the object.
     * .....
     * .....
     * @throws Throwable the {@code Exception} raised by this method
     * @see java.lang.ref.WeakReference
     * @see java.lang.ref.PhantomReference
     * @jls 12.6 Finalization of Class Instances
     */
    protected void finalize() throws Throwable { }
```







## 结束语

使用Happen-before规则，更多的是通过这一系列的规则，**限制CPU的缓存和编译器优化**，进而解决并发带来的**新问题**。主要解决的问题是**可见性和有序性**。

最后，说一点新的发现吧！

其实并发涉及的知识还是很多的，一嘴一个大胖子是行不通，唯有理清楚思路，明白原理，对应的使用代码进行试验。才是一条缓慢而上升的道路。

下一篇，我们将看看Java中的原子性问题，也即锁。












