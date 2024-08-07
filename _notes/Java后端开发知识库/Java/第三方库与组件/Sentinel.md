---
createDate: 2024-08-05
createTime: 2024-08-05 09:31
type: entity
tags:
  - K/CS/java
  - K/CS/web
  - K/CS/SpringCloud
father:
  - "[[第三方库与组件]]"
aliases: 
ref: 
project: "[[Project IM netty 造轮子]]"
---
Summary::
sentinel顾名思义：卫兵；在Redis中叫做**哨兵**，用于监控主从切换，但是在微服务中叫做**流量防卫兵**。

Sentinel 以流量为切入点，从**流量控制**、**熔断降级**、**系统负载**保护等多个维度保护服务的稳定性。

Sentinel 具有以下特征:

- **丰富的应用场景**：Sentinel 承接了阿里巴巴**近 10 年的双十一**大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。
    
- **完备的实时监控**：Sentinel 同时提供实时的监控功能。您可以在控制台中看到接入应用的单台机器秒级数据，甚至 500 台以下规模的集群的汇总运行情况。
    
- **广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与 Spring Cloud、Apache Dubbo、gRPC、Quarkus 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。同时 Sentinel 提供 Java/Go/C++ 等多语言的原生实现。
    
- **完善的 SPI 扩展机制**：Sentinel 提供简单易用、完善的 SPI 扩展接口。您可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。
# 参考文章
[微信公众平台](https://mp.weixin.qq.com/s?__biz=MzU3MDAzNDg1MA==&mid=2247498039&idx=1&sn=3a3caee655ff015b46249bd51aa4dc79&chksm=fcf726facb80afecea4d48faf94a9940b80ba21b325510cf4be6f7c7bce2f3c73266857f65d1&scene=21#wechat_redirect)
