# MongoDB 是什么？

* MongoDB 将数据储存在灵活，类似JSON(BSON) 的文档中，这意味着字段可以随着文档的不同而变化，数据结构可以随着时间的推移而改变。

* 文档模型映射到应用程序代码中的对象，使数据易于实用


* MongoDB 是一个分布式数据库的核心，因此，高可用性，水平缩放，地理分布是内置的，易于实用

* MongoDB 是自由和开源的，出版根据GNU Affero 通用公共许可证

# 什么是 BSON

BSON是一种类json的一种二进制形式的存储格式，简称Binary JSON，它和JSON一样，支持内嵌的文档对象和数组对象，但是BSON有JSON没有的一些数据类型，如Date和BinData类型

# MongoDB 优劣

### 优势：

* 高可用，支持自动故障恢复（副本集）
* 比关系型数据库更高的写入负载
* 支持大容量的存储，内置 Sharding 分片简单
* 海量数据下，性能优越
* 支持地理位置查询

### 缺点

* 不支持事务操作
* 占用空间大
* 不支持关联表查询
* 自由灵活的文件存储格式带来的数据错误

# MongoDB 适用场景

频繁的写入操作，不可靠环境保证高可用性，数据规模大(如预估会超过5G的数据量)，数据结构变更频繁。如(爬虫，日志记录，监控记录等)

# MongoDB 安装

* 下载安装 MongoDB https://www.mongodb.com/download-center?jmp=nav#community

# MongoDB 主要程序介绍

* mongod ： MongoDB 服务器
* mongo ： 进入 MongoDB 命令行
* mongodump ： MongoDB 数据库备份（导出格式为 .bson ）
* mongorestore: MongoDB 数据库恢复
* mongoexpoort ： MongoDB 数据导出（导出格式为： .json  .csv）
* mongoimport ： MongoDB 数据导入 （导入格式为：CSV, TSV or JSON）
* mongotop, mongostat: MongoDB 监控工具
