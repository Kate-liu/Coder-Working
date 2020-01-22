



# 社交公司们的大数据贡献

在 Hadoop 诞生初期，雅虎扮演了“活雷锋”的角色，几乎凭借一己之力撑起了整个 Hadoop 系统的发展。2006 年雅虎把 Hadoop 开源以后，其他公司渐渐加入了 Hadoop 生态圈，其中三大社交公司 Facebook、LinkedIn 和 Twitter 的加入，为 Hadoop 生态圈的繁荣发展做出了巨大贡献。

## 一、Facebook 对 Hadoop 生态圈的贡献

最先加入雅虎 Hadoop 项目里的是还在创业阶段的 Facebook，它从 2008 年开始在内部使用 Hadoop。**因为用 MapReduce 做数据分析需要写很多 C++ 或者 Java 程序，这非常不方便，因此 Facebook 决定做一个叫作 SQL on Hadoop 的项目，也就是后来鼎鼎大名的 Hive。** 这个项目的目标是，要在 Hadoop 上搭建一个可以用类似 SQL 进行数据查询、分析的应用。

最开始的时候，Facebook 内部专门成立了一个 Hive 团队，后来团队成员从最初的两个人扩展到六个人。这时，Hive 项目只是 Facebook 一个公司在开发和推广。

Hive 的开发风格体现了 Facebook 的特色：快、糙、猛。Hive 开发者的代码写得很快，因此 Hive 的代码质量是所有开源软件里面相对比较粗糙的：Bug 比较多，且维护难度大，但基本上实现了所有必需的功能。如果说在没有遇到 Bug 且不需要维护的情况下，Hive 还是可以凑活着用的。

但 Hive 后来的发展走向不再是 Facebook 来主导了，究其原因有以下两个。

1. Facebook 不断撤出对 Hive 的投资。一方面，Hive 团队纷纷出走；另一方面，Facebook 把开发重心转移向另外一个新的内部工具 Presto。Presto 后来也被 Facebook 开源，并被包括 Airbnb、美团、京东等诸多企业采用。
    这种变化的主要原因是 Facebook 内部的赛马机制，Presto 团队在产品上取得了胜利，从而可以获得越来越多的资源。而 Hive 团队获得的资源越来越少，无法再支撑其继续发展。
2. Hive 是最像 SQL 语言的，也是最方便的，因此，Hadoop 的发行商们纷纷加入 Hive 项目的开发和维护，这其中对 Hive 最为青睐的就是 Cloudera 和从雅虎出来的 Hortonworks。所以，2011 年以后 Hive 项目就渐渐地由 Facebook 主导变成由这两个公司主导了。

**Facebook 的另外一个贡献是，开源了 NoSQL 数据库项目：Cassandra。** Cassandra 项目最初是由 Facebook 开发的，其实是效仿了亚马逊的 Dynamo。但后来 Facebook 却转投了 HBase 的怀抱，而任由 Cassandra 自生自灭。

这个决定是当时 Facebook 的一位高管做的，具体是哪位高管无从查证，但这个决定背后的动机很明显，因为 Facebook 觉得谷歌的架构（HBase 是谷歌 BigTable 的山寨版）更可靠，而对亚马逊的架构信心不足。

Cassandra 的发展因此出现了一段时间的停滞，直到 DataStax 接手 Cassandra 项目。有关 Cassandra 的故事，我会留到讲 DataStax 的时候再详细介绍。

而 Facebook 投奔的 HBase，也是 Hadoop 生态圈非常重要的成员，由已经被微软收购的公司 Powerset 贡献。HBase 的故事，我会留到讲 Powerset 的时候再详细展开。

## 二、LinkedIn 对 Hadoop 生态圈的贡献

LinkedIn 是一家主导社交、求职的媒体公司，也是很早就开始用 Hadoop 去做内部数据的分析。它早年和 Facebook、IBM 等公司一起给 Hadoop 贡献了不少源代码，对 Hadoop 整个生态圈的发展做出了巨大贡献。

**LinkedIn 对 Hadoop 做出的巨大、原创性的贡献是其开源项目 Kafka。** 简单地说，Kafka 是一个在不同数据源之间进行数据交换的消息队列的实现。这个项目由 LinkedIn 首创，是一个目前为止在整个 Hadoop 生态圈里都无可替代的开源项目。

Kafka 诞生的背景是，LinkedIn 内部有很多不同的数据源，而且 LinkedIn 需要在这些数据源之间进行有效的数据整合工作。这个项目被 LinkedIn 开源后备受关注，LinkedIn 也因此获得了很多关注。

创业的诱惑可能是每个成功项目的创始人们都无法拒绝的，Kafka 的创始人们也没能免俗。于是在 2014 年，Kafka 的创始人们离开了 LinkedIn，并创办了 Confluent，致力于 Kafka 的商业化使用。有关 Kafka 的详细情况，留待讲 Confluent 的时候我再详细叙述。

**LinkedIn 另一个著名的开源项目是流处理引擎：Samza。** Samza 和 Kafka 的搭配使用，是 LinkedIn 内部流数据的实时查询标配的解决方案，一直支撑着 LinkedIn 业务的发展。遗憾的是，跟 Kafka 比起来，Samza 的名气相差甚远，最重要的原因就是 Samza 没有另外一个社交公司 Twitter 的流处理引擎 Storm 好用。

## 三、Twitter 对 Hadoop 生态圈的贡献

对 Hadoop 生态圈有着巨大贡献的另外一家社交公司是 Twitter，它最重要的贡献是：开源的流处理引擎 Storm。严格来说，最初开发 Storm 的并不是 Twitter，而是一家叫作 BackType 的初创公司。Twitter 收购 BackType 以后，Storm 自然就属于 Twitter 了。Storm 在 Twitter 手中被发扬光大，并开源出来。

Hadoop 本身是用 Java 开发的，所以这个生态圈里的大部分项目都基于 Java 语言，但 Storm 却是用比较小众的语言 Clojure 开发的，这也是 Storm 项目的特殊性。熟悉 Clojure 这个语言的程序员很少，因此想要找出一个写 Clojure 比较出彩的程序员并不是一件容易的事情，这也就导致了 Storm 的开发圈子要相对封闭一些。

但是，开发圈子的封闭性并没有影响 Storm 被广泛接受和使用。在很长一段时间里，Storm 都是进行流计算的首选引擎。

Storm 也被国内的大公司广泛采用，用得最多的要属阿里巴巴了。作为全球最大的电商，阿里巴巴的流数据处理规模很快就超越了 Storm 可以处理的范围，因此它必须自己对这个开源项目进行优化、改进。

然而 Storm 使用的开发语言是 Clojure，这个语言本来就比较小众，国内可以熟练使用这个语言的人更是罕见，于是阿里巴巴的团队把整个 Storm 的引擎又用 Java 重新写了一遍，并将其命名为 JStorm。JStorm 后来被阿里巴巴集团捐给了 Apache 软件基金会，成为了 Storm 项目下面的一个子项目。

不过，近些年来随着 Spark 对流计算的支持和 Flink 的异军突起，流计算的开源市场又有点风起云涌的感觉了。有关 Spark 的内容，我会在 Databricks 的文章里面详细讲解。有关 Flink 的内容，我会在 data Artisans 的文章里详细讲解。

**总结来说，在 Hadoop 从属于雅虎一家公司到逐渐被硅谷的其他互联网公司接受、再到形成生态圈的过程中，Facebook、LinkedIn 和 Twitter 这三大社交媒体公司对 Hadoop 的贡献是巨大的。**

如果没有这么多公司投入这么多资源去完善 Hadoop，并通过各种开源项目解决整个生态圈缺失的功能，那么 Hadoop 很难成长到今天这样的规模。现在，Hadoop 已经不仅仅是一个大数据平台了，更代表了一种标准。在今天，无论什么企业要提供什么样的产品，都需要兼容 Hadoop 生态圈。

不过，这些社交公司对 Hadoop 生态圈的热衷，也可以说是因为这些公司单独的技术实力不够强大、难以和谷歌抗衡，因此抱团取暖、共同促进和完善这个生态圈，是它们和谷歌并存的不二法门。

因此，**Hadoop 的诞生，可以说是天时、地利、人和的必然产物。** 在我看来，即使没有 Hadoop，也会在相似的时间点、在某一群公司的共同努力下，诞生一个类似 Hadoop 的项目。











































