# Cassandra和DataStax的故事

Cassandra 是大数据时代中非常具有影响力的一个开源项目，DataStax 则是背后支持开源 Cassandra 并将其商业化的公司。今天我们就来聊一下 Cassandra 和 Datatax 的故事。

我们都知道，在大数据发展历史上，谷歌的“三驾马车”：谷歌文件系统、 MapReduce、 BigTable。三者都曾经扮演了非常重要的角色，Hadoop 开源生态圈里也有对应的 Hadoop 文件系统，Hadoop MapReduce 和 HBase。

但是在大数据发展史上，还有一篇影响力几乎等同于谷歌“三驾马车”的论文。它讲的就是亚马逊发布的 Dynamo 系统。

2008 年，Dynamo 系统的作者之一阿维纳什·拉克希曼（Avinash Lakshman），跳槽去了 Facebook。跳槽的阿维纳（Avinash）和 Facebook 网站的另外一个工程师普拉桑特·马利克（Prashant Malik），一起开发了 Cassandra，一个 Dynamo 的开源山寨版。

Cassandra 开发出来之后很快就被开源了。早期 Facebook 对于开源这件事还是非常支持的，但是它开源的 Cassandra 很快就受到了一次重大的打击，这个打击可以说是十分致命的。

早年的 Facebook 对于谷歌技术非常崇拜，但对于亚马逊的技术却缺乏信心。于是 Facebook 准备开发移动 App“Messenger”的时候，决定使用谷歌的技术架构。更明确一点说就是，Facebook 抛弃了自己开发的 Cassandra，选择了当时在 Hadoop 系统里山寨了 BigTable 的 HBase。

亲儿子被自己的公司抛弃，开发人员也没什么兴趣继续开发了。与被众心捧月的 HBase 状态比起来，Cassandra 当时就是一种被众人嫌弃的状态，不过，如果故事到此为止的话，那么 Cassandra 估计也就不会活到今天了。

我们把时光回溯到 2010 年，当时在 Rackspace 工作的乔纳森·艾利斯（Jonathan Ellis）和马特·皮菲尔（Matt Pfeil），这两个和 Cassandra 无关的人，决定离开 Rackspace，自己创业。

Rackspace 在工业界里最为著名的是 OpenStack 那一套体系，做的是数据中心云计算的基础架构。算起来和 Cassandra 这套 NoSQL 的东西多少也有点关系。

他们创业的故事非常有意思，同时也跟 Cassandra 有着千丝万缕的联系，公开的说法是这样的。

> 乔纳森是个很牛的工程师，决定结束碌碌无为的工作状态，辞职创业去。马特代表公司去挽留这个人才，于是两个人约了去吃午餐；然而结局却颇为戏剧化，马特没有说服乔纳森继续为 Rackspace 工作，而杰纳森却说服了马特和他一起创业，并让他出任自己公司的 CEO。
> 公司同年成立，最初公司的名字叫 Riptano。创业需要有方向，乔纳森和马特看好开源社区商业化的模式，但是他们并没有打算成为 Hadoop 的发行商，所以环顾四周之后他们挑中了 Cassandra，并打算将它做为核心，开启他们的创业之旅。
> 大概就是因为选取了 Cassandra，公司的定位就比较明确了，也就是选择了云端数据处理的方向。于是他们觉得 Riptano 这个公司的名字不太适合公司的定位，就把公司名字改成了 DataStax。这个故事就是 DataStax 的由来。

自从 2010 年选中了 Cassandra 之后，DataStax 就开始了全力以赴开发 Cassandra 的历程。在很长一段时间里，DataStax 对 Cassandra 贡献的代码量，占据了整个代码提交量的 85% 以上。

可以说，正是因为 DataStax 的介入，才最终让 Cassandra 活了下来，并且在 2011 年成为了 Apache 基金会的顶级开源项目。DataStax 推出的主打产品，是一个叫做 DataStax Enterprise 的东西。这是一个以 Cassandra 为核心，整合了诸多开源项目的产品。

DataStax Enterprise 提供了两种模式，一种是卖软件和服务给企业，企业再装到自己的机器上去运行。另外一种是托管云服务“DataStax Managed Cloud”，这是一个运行在亚马逊云服务（AWS）上的云托管服务，用户无需购买和维护自己的机器。

从产品完整性和盈利模式来看，DataStax 提供的是相对来说比较完整的一套产品体系。但是以 Cassandra 为核心的主要问题是，Cassandra 的技术相对冷门，优点和缺点也都很明显，这导致的结果是：适用于 Cassandra 的应用也是有一定限制的。

DataStax 的产品也因为选择了 Cassandra 作为核心，和其他公司的同类产品就有很明显的不一样。

具体来说，Cassandra 是一个写入非常快、吞吐量很大、延时很低的系统；同时，这个系统的处理能力伴随容量的增长，也呈现出线性的增强。这些都是 Cassandra 的优势。尤其是做云端部署时，这个系统可以很灵活地根据工作负载来加减机器。

2012 年，多伦多大学一篇论文比较研究了 6 个不同的 NoSQL 数据库的优劣，得出的结论是 Cassandra 是当之无愧的赢家。这篇论文被 DataStax 广泛引用，以此来证明这个系统比其他更为优质。

但是凡事都有两面性，Cassandra 的缺点也很明显。首先是 Cassandra 有一个十分令人讨厌的问题：这个系统没办法保证一条记录行级别的一致性。

简单来说，如果 A 操作改变了行里面的一个列，B 操作改变了同一行里面的另外一列，那么很有可能就得到了一条四不像的行。

这对应用程序来说是一件非常糟糕的事，虽然现实来说这种错误的概率不是特别高，但是只要不是 0 概率的话，很多应用程序都不可能使用这样的系统。

还有一个缺点是 Cassandra 普遍适用的场景非常有限，Cassandra 虽然对于单行操作非常快，但是对于多行操作就会非常慢；而且不仅仅慢，很可能同时消耗的资源也会很高。

Cassandra 对范围查询的能力比起 HBase 要差了很多。因此，通常来说 Cassandra 应用的场景适合只访问单行记录的，但是在单行记录的时候却不能保证行级别的一致性。这就是 Cassandra 适用场景的瓶颈所在。

不过，DataStax 发展到了今天，它的主打产品 DataStax Enterprise 也是经过了多年的演进，并且在以 Cassandra 为核心的基础上，进行了全面的整合。

例如它通过对 Spark 和 Solr 的整合，提供了数据分析和搜索的功能。它还在自我完善中提供了对多种语言和开发平台的支持，比如说 Java、Python、Ruby、 C++、Javascript 等等。

此外，DataStax Enterprise 还提供了给管理员用来做系统监控和操作的 OpsCenter，以及给开发者提供的 IDE 环境 DataStax Studio。

从产品的完善程度来讲，DataStax Enterprise 是非常完善的，它是一套整合了开源以及自主开发产品的系统，并提供了开发、运行、部署和监控几乎全方位的支持。这些都是这套系统的优势。

然而，DataStax 的发展相对来说不温不火，在业界也只是名气平平。我想，它选择了 Cassandra，既给了 DataStax 足够多的辨识度和区分度，也让 DataStax 的产品受到了各种限制。至于这样的选择到底是好是坏，对 DataStax 的发展是否有利，可能只有时间才能说清楚了。

不管怎么样，Cassandra 仍然需要感谢 DataStax 的救命之恩和鼎力支持。可以说没有 DataStax，就不会有今天的 Cassandra。















































