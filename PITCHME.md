# RabbitMQ

工作交接

---

### Agenda

- why RabbitMQ ?
- RabbitMQ Cluster
- RabbitMQ HA
- RabbitMQ运维问题

---
### Why RabbitMQ ?

- 核心问题
  * 解决消息传递的问题

- 架构问题
  * 改变消息传递方式
  * 灵活、可靠

---

### RabbitMQ Cluster
- 目标
  * 整个集群对外就像一个RabbitMQ服务
  * RabbitMQ集群是永不宕机的
- 如何实现？
    * 共享路由信息（exchange & binding rules）
    * 内部的proxy
    * 消息持久化、多副本

---
### RabbitMQ HA
- 实现方法：Cluster + Mirror Queue
- Cluster实现 路由信息的共享
- Mirror Queue 实习消息的高可用

---
### RabbitMQ底层存储

---
### RabbitMQ Mirror Queue (1)
- 实现原理
  * 一主多从
  * 消息依次传递经过所有节点

---
### RabbitMQ Mirror Queue (2)
- 设置方法

```bash
$ rabbitmqctl set_policy rabbitmqctl set_policy HA '^(?!amq\\.).*' '{"ha-mode":"all","ha-sync-mode":"automatic"}' --apply-to queues

$ rabbitmqctl list_policies
Listing policies ...
/	HA	queues	^(?!amq\\\\.).*	{"ha-mode":"all","ha-sync-mode":"automatic"}	0
```

---
### RabbitMQ运维(1)
- 每个队列只能有一条policy

---
### RabbitMQ运维(2)
- 集群所有的节点同时关机后无法启动

---
### RabbitMQ运维(3)
- 内存占用太高导致无法push消息

---
### RabbitMQ运维(4)
- Web控制面板
- 命令行工具

---
### 必看资料
- [RabbitMQ Cluster](https://www.rabbitmq.com/clustering.html)
- [RabbitMQ HA](https://www.rabbitmq.com/ha.html)
