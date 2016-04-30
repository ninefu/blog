title: How to Design the backend of WeChat
date: 2016-01-20 22:39:05
categories: 
- System Design
tags:
- System Design
comments: true
---

Notes from Tiger's Lecture

# How to communicate between two users?

Client Server model

```
User 1 <== connection ==> User 2

(How to know where is the other guy? TCP/IP. But how to know the IP address? ===> server. If there is no server,  we can use MAC. Why use IP instead of MAC? MAC地址可以修改， 同时没有搭配的协议栈. If there is no server or IP, use P2P.)
```

### How to connect

```
A  <==> B 

mail model: short connection
phone model: persistent connection （每个 router 都记录 A-B 的路径，不需要每次都传递具体通信的 meta 信息）
```

### Could we build WeChat without Server

### How to save traffic

1. user persistent connection
2. P2P 不稳定 & 法律监管 & 带宽环境变好
2. 批量压缩
3. web socket in http

pull push model 消息延迟加载，先推送新消息的计数，等打开 app 才刷新消息的具体内容，如果消息多的话还可以压缩以便进一笔节省流量

### What data need to be save in client

1. message
2. account
3. contacts

### Sync between two clients (mobile/desktop)

timestamp，但是用户的时间可能是错的，所以用逻辑时钟/版本号
user pull version or server push

# How to build API

Scenario
1. send message
2. account
3. read message
4. 红包
5. log in/out
6. 朋友圈
7. location

=> chat, account, feed

client ==> 顶层业务 API ==> 逻辑 API / DATA API （可并行串行，微信用并行） ==> DATA

### How to communicate between services?

common gate way interface

```
API
||
||
\/
a large container determines which module should API go to

缺点：耦合，单点故障，连带效应（故障/升级）
```

```
Micro service
底下的服务每个都提供一个 http 接口，每个都是独立的，在 master 那里注册一下，多个 master。每个都是单独的进程
```

### How to support QQ message

### How to support group chat
异步 RPC
disruptor

设计广播/feed模式

假设群内有 u1 u2 u3，群发就是 u1-u2,u1-u3,...,etc，而不是 u1-channel （逻辑复杂），微信群设人数上限

### How to configure API

# How to store data

1. message
2. account
3. contacts

### Should we save them together
### What is the key

1. message, NoSQL
2. account, SQL
3. contacts, SQL

### Why do we need memory
在内存里进行复杂的 join 等操作

### Is one data center enough
容灾

### How to monitor the number of registered users
MySQL count

### How to monitor the number of online users
log,上线了就+1离线了就-1，注意掉线的情况

### How to notify the numbers to team

### What are the steps for log
分布式 log
1. log统计代码
2. 保存在本地或者发送到 log server 上 （每台机器上有个进程专门处理 lock，加减等操作）
