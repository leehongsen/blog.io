---
layout: post
title: Java简单分页算法
date: 2018-10-19
categories: blog
tags: [技巧,记录]
description: 3个最常用的Java分页算法。
---

 1. 最常用最简单版   
``` javascript
//总记录数
int rows=21;  
//每页显示的记录数
int pageSize=5;  
//页数
int pageSum=(rows-1)/pageSize+1;`
``` 

 2. 三目运算符版   
``` javascript
//总记录数
int rows=21;  
//每页显示的记录数
int pageSize=5;  
//页数
int pageSum=rows%pageSize==0?rows/pageSize:rows/pageSize+1;
```

 3. 化简版   
``` javascript
//总记录数
int rows=21;  
//每页显示的记录数
int pageSize=5;  
//页数
int pageSum=(rows+pageSize-1)/pageSize;
```

欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过 `小书匠主按钮>模板` 里的模板管理来改变新建文章的内容。