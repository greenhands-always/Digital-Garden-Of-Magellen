---
layout: page
title: Home
id: home
permalink: /
---
Hi，我是Magellen，一个新手开发者。
欢迎来到的我的博客，这里是我的个人知识库，关注程序员精进、效率工具、个人成长。


**持续更新：**

[飞书知识库：不可替代：大颠覆时代的生存之道](https://kv57sk4imd.feishu.cn/wiki/F36EwpIsDiSZCdk9aSecgl9Qnnd?fromScene=spaceOverview)

[[快速下班指南]]：致力于提高个人效率。

[[Java后端开发知识库]]

[计算机学习过程demo代码仓库](https://gitee.com/greenhands99/computer-system-learning-demo)

**最近创建：**

{% assign recent_notes = site.notes | sort: "date created" | reverse %} {% for note in recent_notes | limit: 6 %}- {{ note['date created']}} — [{{ note.title }}](https://github.com/oldwinter/dg/blob/master/_pages/%7B%7B%20note.url%20%7D%7D)
{% endfor %}

**最近更新：**

{% assign recent_notes = site.notes | sort: "date modified" | reverse %} {% for note in recent_notes | limit: 6 %}- {{ note['date modified']}} — [{{ note.title }}](https://github.com/oldwinter/dg/blob/master/_pages/%7B%7B%20note.url%20%7D%7D)
{% endfor %}