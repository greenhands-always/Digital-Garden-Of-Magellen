---
createDate: 2024-07-31
createTime: 2024-07-17 18:53
type: index
father:
  - "[[计算机网络]]"
  - "[[Java]]"
tags:
  - MOC
  - K/CS/java
aliases: 
MapLevel: 
project: "[[Project IM netty 造轮子]]"
permalink: /java/netty
---
# 内容地图
## 子地图
```dataviewjs
const fileName = dv.current().file.name;  
const result =  dv.execute(`table father from [[${fileName}]] where contains(tags, "MOC") and !contains(file.path, "template")`);
```
## 关联文章
```dataviewjs
const fileName = dv.current().file.name;  
const result =  dv.execute(`table father from [[${fileName}]] where !contains(tags,"MOC") and !contains(file.path,"template")`);
```

# 简介
Netty是由JBOSS提供的基于[[NIO]]的开源框架，Netty提供异步非阻塞、[[事件驱动架构|事件驱动]]、高性能、高可靠、高可定制性的网络应用程序和工具，可用于开发服务端和客户端。

## 优点
> - API使用简单，更容易上手，开发门槛低
> - 功能强大，预置了多种编解码功能，支持多种主流协议
> - 定制能力高，可以通过ChannelHandler对通信框架进行灵活地拓展
> - 高性能，与目前多种NIO主流框架相比，Netty综合性能最高
> - 高稳定性，解决了JDK NIO的BUG
> - 经历了大规模的商业应用考验，质量和可靠性都有很好的验证。
> [为什么要用Netty开发？\_为什么要用netty编写udp-CSDN博客](https://blog.csdn.net/xu_melon/article/details/79201198)