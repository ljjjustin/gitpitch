# RabbitMQ

工作交接

---

### Agenda

- Why RabbitMQ?
- RabbitMQ 101
- RabbitMQ HA
- RabbitMQ运维问题

---
### Why RabbitMQ ?

- 核心问题
  * 可靠的消息传递
  * 场景
    - 证券交易所
    - 微信、QQ ...

---
### Why RabbitMQ ?
- 架构问题
  * 灵活、可靠
    - 传统的C/S模型不够灵活

  * 改变消息传递方式和规则
    - 单播、广播
    - 发布订阅

---
### RabbitMQ 101

- 基本概念
  * exchange、binding、queue

- 消息的传递方式
  * 生活中的邮政系统、email系统

---
### RabbitMQ 101(2)

- 如何保证消息的可靠传输
  * broker：publish Confirm
  * receiver ACK

---
### RabbitMQ HA
- 实现方法：Cluster + Mirror Queue
- Cluster实现 路由信息的共享
- Mirror Queue 实现消息的高可用

---
### RabbitMQ Cluster(1)
- 目标
  * 对外就像单节点的RabbitMQ服务
  * RabbitMQ集群是永不宕机的
  * 没有消息丢失

---
### RabbitMQ Cluster(2)
- 如何实现？
    * 共享路由信息（exchange & binding rules）
    * 消息持久化、多副本
    * 内置的proxy(单节点push消息，任意节点读消息)

---
### RabbitMQ Mirror Queue (1)

- 实现原理
  * 一主多从
  * 消息依次传递经过所有节点

---
### RabbitMQ Mirror Queue (2)

- 设置方法

```bash
$ rabbitmqctl set_policy rabbitmqctl set_policy \
HA '^(?!amq\\.).*' '{"ha-mode":"all","ha-sync-mode":"automatic"}' --apply-to queues

$ rabbitmqctl list_policies
Listing policies ...
/	HA	queues	^(?!amq\\\\.).*	{"ha-mode":"all","ha-sync-mode":"automatic"}	0
```

---
### RabbitMQ底层存储
- mnesia
  * 基于erlang实现的高可扩展的数据库管理系统

---
### RabbitMQ运维(1)
- 每个队列只能有一条policy
  * 后续的policy会覆盖前面的policy

---
### RabbitMQ运维(2)
- 集群所有的节点同时关机后无法启动

```bash
$ rabbitmqctl forget_cluster_node --offline
```

---
### RabbitMQ运维(3)
- 内存占用太高导致无法push消息
  * 消息堆积
  * 连接数太多（没有正确关闭）

---
### RabbitMQ运维(4)
- Web控制面板
  * [demo](http://10.70.238.48:15672/)
- 命令行工具
  * rabbitmqctl: 直接与mnesia数据库进行交互
  * rabbitmqadmin: 基于管理插件提供的REST API

---
### 必看资料
- [RabbitMQ HA](https://www.rabbitmq.com/ha.html)
- [RabbitMQ Cluster](https://www.rabbitmq.com/clustering.html)
