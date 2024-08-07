---
createDate: 2024-08-04
createTime: 2024-08-04 14:08
type: index
father: 
tags:
  - MOC
  - K/CS/java
aliases: 
MapLevel: 
permalink: /java/guava
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

[Google Guava官方教程（中文版） | Google Guava 中文教程](https://wizardforcel.gitbooks.io/guava-tutorial/content/1.html)

# 简介
Guava是一款由Google开发的开源Java工具库，它旨在为Java开发者提供一整套强大的工具和实用功能，以简化日常编码任务、提高性能、构建线程安全的应用以及处理文本操作。
## Guava的优点
- 高效设计良好的API，被Google的开发者设计，实现和使用
- 遵循高效的java语法实践
- 使代码更简练，简洁，简单
- 节约时间，资源，提高生产力
## 源码结构
com.google.common.annotations：普通注解类型。
com.google.common.base：基本工具类库和接口。
com.google.common.cache：缓存工具包，非常简单易用且功能强大的JVM内缓存。
com.google.common.collect：带泛型的集合接口扩展和实现，以及工具类，这里你会发现很多好玩的集合。
com.google.common.eventbus：发布订阅风格的事件总线。
com.google.common.graph：对“图”数据结构的支持。
com.google.common.hash： 哈希工具包。
com.google.common.io：I/O工具包。
com.google.common.math：原始算术类型和超大数的运算工具包。
com.google.common.net：网络工具包。
com.google.common.primitives：八种原始类型和无符号类型的静态工具包。
com.google.common.reflect：反射工具包。
com.google.common.util.concurrent：多线程工具包。
com.google.common.escape：提供了对字符串内容中特殊字符进行替换的框架，并包括了Xml和Html的两个实现。
com.google.common.html：HtmlEscapers封装了对html中特殊字符的替换。
com.google.common.xml：XmlEscapers封装了对xml中特殊字符的替换。
# 参考文章
[Guava：Java开发者的全方位工具库\_guava java-CSDN博客](https://blog.csdn.net/Mrxiao_bo/article/details/134291893)