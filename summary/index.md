# Elasticsearch介绍
> Elasticsearch是一个高度可扩展的开源全文搜索和分析引擎,它允许你快速，近实时地存储，
搜索和分析大量数据，它通常用作底层引擎/技术，为具有复杂搜索功能和要求的应用程序提供支持

## 基本概念
### 近实时
> Elasticsearch是一个近乎实时的搜索平台。这意味着从索引文档到可搜索文档的时间有一点延迟（通常是一秒）
### cluster
>* 集群是一个或多个节点(node)的集合, 他们共同保存整个数据，并提供跨所有节点的联合索引和搜索。
>* 集群有一个唯一的名称用来作为标识，默认名称为"elasticsearch"。
>* 名称很重要，因为如果节点(node)设置为按名称加入集群，则该节点只能是改名称对应的集群的一部分。确保不要在不同的环境中重用相同的集群名称，
否则最终会导致节点加入到错误的集群。
>* 注意，拥有一个只包含单个节点的集群是正常的，也就是说就算是只有一个节点，那么也会存在一个集群，默认名称为"elasticsearch"，简而言之，集群一定会存在。
### node
>* 节点是集群中的单个elasticsearch服务器，存储数据并参与集群的索引和搜索功能。
>* 向集群一样，集群中的节点也有一个名称唯一标识，默认情况下，该名称实在启动时分配给节点的随机通用唯一标识符(UUID)。你也可以自己定义节点的名称。此名称对于管理目的非常重要，您可以在其中识别网络中的哪些服务器与Elasticsearch集群中的哪些节点相对应。
>* 节点可以配置为按名称加入集群，默认情况下，节点会加入集群名称为"elasticsearch"的默认集群，也就是说，如果创建个多个节点，并且多个节点之间可以互相发现，则
它们会自动注册到名称为"elasticsearch"的默认集群中。
>* 在单个集群中可以拥有任意数量的节点，如果只使用了一个节点，默认情况下，启动的单个节点将形成一个名为elasticsearch的新单节点集群
### index
>* 索引是具有某些类似特征的文档(document)的集合, 例如，您可以拥有客户数据的索引，产品目录的另一个索引以及订单数据的另一个索引。相当于数据库中的一个表结构。
>* 索引由名称唯一标识，名称必须全部小写。并且此名称用于在对其中的文档执行索引，搜索，更新和删除操作时引用索引。
>* 在单个集群中，可以根据需要定义任意数量的索引。
### type
>* 类型，曾经是索引的逻辑类别/分区，允许您在同一索引中存储不同类型的文档，例如用户的一种类型，博客帖子的另一种类型。
>* <span style="color: red">不再可能在索引中创建多个类型，并且将在更高版本中删除类型的整个概念</span>
### document
>* 文档是可以索引的基本信息单元，例如，您可以为单个客户提供文档，为单个产品提供另一个文档，为单个订单提供另一个文档。相当于数据库中的一条记录。
>* 文档中的数据以JSON数据格式来保存, 在单个index/type中可以保存任意数量的文档。
>* 请注意，尽管文档实际上位于索引中，但实际上必须将文档索引/分配给索引(index)中的类型(type)。
### Shards & Replicas
