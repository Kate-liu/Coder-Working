





# Databricks之Spark的数据金砖王国

说起大数据的创业公司，我们一定都会提到 Databricks 这公司，而这家公司知名的原因，一大部分来自于它的开源产品 Spark。Spark 是 Hadoop 生态圈里大红大紫的项目，事实上，它甚至已经取代了新一代的经典运行框架：Hadoop MapReduce。

所以，想要了解 Databricks 这家创业公司，我们就需要先了解 Spark 这个 Apache 开源项目。Spark 是一个大数据计算框架，它诞生于加州大学伯克利分校 AMP 实验室，是当时的博士生马泰·扎哈里亚（Matei Zaharia）的博士论文课题。

2010 年，Spark 在 BSD License 下开源。经过几年发展以后，在 2013 年成立了 Databricks，同年，它被 Databricks 捐献给 Apache 基金会，并将开源模式转向了 Apache 2.0，从此，Spark 正式成为 Apache 家族里顶级开源项目之一。

Spark 是目前整个 Hadoop 的生态系统里最为活跃的计算框架，它已经取代了 Hadoop 原来 MapReduce 框架的地位，目前，只有 Flink 的计算框架尚能与它平分秋色（有关 Flink 的情况，我们会在后面的文章里详细介绍）。

Spark 框架下支持 SQL、机器学习、图计算、流计算等各种各样的计算模型，应用起来十分广泛。它不仅在开源社区里广受追捧，在大公司里也常常被拿来应用，IBM 现在已经把自己的大数据计算引擎押宝在 Spark 上了。

介绍完 Spark，我们来看看它背后的 Databricks 公司，这家公司是由加州大学伯克利分校 AMP 实验室的原班人马组建的，它成立的目的主要是为了推广 Spark 和 Spark 的生态圈。

Databricks 的管理层可谓明星荟萃。CTO 马泰·扎哈里亚是 Apache Spark 最初的创作者，同时也是斯坦福大学的教授。CEO 是阿里·格霍西（Ali Ghodsi）是加州大学伯克利分校的兼职教授，执行总裁艾恩·斯塔卡（Ion Stoica）也是学校的全职教授，他还是 CTO 马泰·扎哈里亚的导师。另外一位联合创始人是华人雷诺·辛（Reynold Xin），他现在是首席架构师。

Databricks 的核心，主要是 Spark。如果我们把 Spark 理解成为一个计算平台的话，那么围绕着 Spark 生态圈做的东西则是 Databricks 的核心价值。对 Databricks 来说，首先要做的事情，是把 Spark 的开源项目越做越大。

作为做大 Spark 的一部分，Databricks 对 Spark 发展方向的掌控在开源社区是出了名的强势。自从 Databricks 成立以来，对 Spark 技术的演进一直都是有自己的路线图的。

近些年来，无论是 SparkSQL、DataFrame 的推出，还是基于 Mini-batch 的 Spark Streaming 的工作开展，都是 Spark 这个计算框架下面非常重要的项目。如果没有 Databricks 的推动和首肯，这些项目几乎不可能进到 Spark 的发行版里。

因此，我们总结一下 Databricks 的商业模式：壮大 Spark 社区，掌控和引导 Spark 的技术走向。

然而仅仅做大 Spark 开源项目，对 Databricks 来说还是不够的，这些不足以带给 Databricks 盈利；而一个公司是否成功，最终还是取决于这个公司的赚钱能力。从这个角度上来讲。壮大 Spark 是 Databricks 盈利的一个基础，但是却不是 Databricks 盈利的根本。

那么说，Databricks 是怎么盈利的呢？

**Databricks 的第一条盈利方式就是：选择在这些基石上面，开发附加产品来赚钱。** 其中第一个产品，也是 Databricks 现阶段正在努力的方向，就是提供云上搭建的 Spark 计算平台。

我们来看看这个产品具体是如何赚钱的。

Spark 团队在一开始设计 Spark 产品的时候，就遵循了一条原则：它和 Hadoop 整个体系保持松耦合，所有的相关服务都抽象成接口，再通过接口调用。

这样做的好处在于，如果 Spark 哪一天决定和另外一套类似的系统对接，那么只要针对另外一套系统重新实现一下接口就好了，Spark 自身的代码则完全不需要改动。

这样，它一方面可以和 Hadoop 做到有效整合，借助业已壮大的 Hadoop 平台和生态圈推广自己。另外一方面，如果万一哪天 Hadoop 被别家取代了，或者 Spark 需要针对某些企业内部系统（比如对微软、谷歌内部大数据系统）进行整合的话，改动工作也会非常容易。

果不其然，深谋远虑的 Spark 团队十分生财有道。他们在开源了支持 Hadoop 的社区版以外，还专门开发了直接对接云厂商的版本，比如亚马逊 AWS 版的 Spark。

这个版本的 Spark 按照 Databricks 公布的数据，针对 AWS 优化的 Spark 的效率比开源版高 5 倍以上，但是，这个版本却不是开源的。

Databricks 又把这个不开源的版本做成云服务卖给用户。由于这个版本的 Spark 比开源版的要更快，很多企业愿意付钱买，这也就成了目前 Databricks 最重要的盈利途径。

**Databricks 的第二条盈利方式是对建立在 Apache Spark 平台上的应用进行认证，并确保这些应用和 Spark 的兼容性。** 这种认证当然不是免费的，由于 Spark 社区的成功，这方面的认证开展工作也是如火如荼。

**Databricks 的第三条盈利方式是：给使用了 Spark 技术的各大公司提供技术支持。** 简单来说，Spark 虽然开源，但是用好 Spark 的公司，不一定都有技术实力读、改源代码来适应自己的应用场景。这个时候买了 Databricks 的技术支持服务的话，Databricks 就可以提供支持了。

由于 Databricks 对 Spark 的源代码非常熟悉，Databricks 的技术支持往往能够解决很多企业非常重要的紧急问题。而有些公司不缺钱，也愿意付钱给 Databricks，这门生意对 Databricks 来说也是重要的赚钱途径。

这三块服务是不是足够支撑 Databricks 呢？我想这个问题的答案有点复杂。

第一块业务非常实际，这是可以大规模推广的赚钱方式。一部分开源，一部分不开源，通过开源来圈用户，通过提供更高性能的服务来赚钱。这个生意做得比较成功。

这个生意里最大的问题是，Databricks 自身并不拥有云平台，它的云平台主要运行在亚马逊的云服务上面，这就造成了亚马逊自己一旦也想做类似服务的话，Databricks 就很难抵抗。所以多做几个云厂商上面的服务，这也许是一个好主意，起码可以不把全部筹码压在一个平台的身上。

后面两块业务的市场取决于 Spark 到底有多重要，以及 Databricks 到底有多懂 Spark。

首先，我觉得 Spark 的重要性毋庸置疑，大企业比如 SAP，IBM 都在其产品里面用 Spark 和引入对 Spark 的支持。这证明了 Spark 的市场占有率是巨大的。

其次，Databricks 的几个创始人基本上奠定了 Spark 的架构。在很多情况下，某些特定的东西 Spark 为什么是这样设计的，也只有做架构的人才能回答了。所以恐怕市面上不存在一家比 Databricks 更懂 Spark 的商业机构。从这一点来看，Databricks 的基本盘是很稳妥的，所以这两个业务也能赚到钱。

但是，Databricks 目前面临的一个大问题是机器学习，尤其是深度学习的潮流。Spark 是用 Scala 写的，并在 JVM 上运行。这就意味着，基于 Spark 的机器学习平台并不能有效地利用 GPU。这样一来，这个问题就大了。

机器学习作为 Spark 最初也是最重要的应用之一，在 Spark 社区占有很重要的地位。Databricks 是否能够有效解决这个问题，对自己的是否能成功和 Spark 将来会怎么发展，都非常的重要。Databricks 的另外一个考验是需要应对 Flink 这个后起之秀的进攻。

我想，Databricks 的前途是光明的，但是也会充满竞争和曲折。









































