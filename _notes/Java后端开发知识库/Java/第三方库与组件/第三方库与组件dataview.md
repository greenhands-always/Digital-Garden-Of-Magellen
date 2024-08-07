---
createDate: 2024-08-05
createTime: 2024-08-05 09:34
type: index
father: 
tags:
  - MOC
  - K/CS/java
aliases: 
MapLevel: 
published: false
---
<div class="hide-in-html"> 这里是只在Obsidian中显示的内容 

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

</div>