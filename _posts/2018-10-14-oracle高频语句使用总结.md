---
layout: post
title: oracle高频语句使用总结
date: 2018-10-14
categories: blog
tags: [技巧,oracle]
description: oracle的使用总结。
---

# oracle高频语句使用总结

## 查询表结构

1. 查询所有表名：  
```select t.table_name from user_tables t;```

2. 查询所有字段名：  
```select t.column_name from user_col_comments t;```

3. __查询指定字段名及描述：（常用）__  
```select t.* from user_col_comments t where t.COLUMN_NAME = '';```

4. 查询指定表的所有字段名：  
```select t.column_name from user_col_comments t where t.table_name = 'BIZ_DICT_XB';```

5. 查询指定表的所有字段名和字段说明：  
```select t.column_name, t.column_name from user_col_comments t where t.table_name = 'BIZ_DICT_XB';```

6. 查询所有表的表名和表说明：  
```select t.table_name,f.comments from user_tables t inner join user_tab_comments f on t.table_name = f.table_name;```

7. 查询模糊表名的表名和表说明：  
```select t.table_name from user_tables t where t.table_name like 'BIZ_DICT%';```
```select t.table_name,f.comments from user_tables t inner join user_tab_comments f on t.table_name = f.table_name where t.table_name like 'BIZ_DICT%';```

8. 查询表的数据条数、表名、中文表名  
```select a.num_rows, a.TABLE_NAME, b.COMMENTS
from user_tables a, user_tab_comments b
WHERE a.TABLE_NAME = b.TABLE_NAME
order by TABLE_NAME;```
```

9. __搜索存储过程（常用）__
```select * from user_source where type='PROCEDURE';```


## 复制表（除oracle以外的数据库）  
1. 复制表结构及数据到新表   
```CREATE TABLE 新表 SELECT * FROM 旧表 ```

2. 只复制表结构到新表   
```CREATE TABLE 新表 SELECT * FROM 旧表 WHERE 1=2 ```  
_即:让WHERE条件不成立._ 

3. 复制旧表的数据到新表(假设两个表结构一样)   
```INSERT INTO 新表 SELECT * FROM 旧表 ```

4. 复制旧表的数据到新表(假设两个表结构不一样)   
```INSERT INTO 新表(字段1,字段2,.......) SELECT 字段1,字段2,...... FROM 旧表```

## Oracle复制表  
如下，表a是数据库中已经存在的表，b是准备根据表a进行复制创建的表：  
1. 只复制表结构的sql 
```create table b as select * from a where 1<>1```

2. 即复制表结构又复制表中数据的sql   
```create table b as select * from a```

3. Oracle复制表的指定字段的sql  
```create table b as select row_id,name,age from a where 1<>1```
前提是row_id,name,age都是a表的列

4. 复制表的指定字段及这些指定字段的数据的sql    
```create table b as select row_id,name,age from a```  
以上语句虽然能够很容易的根据a表结构复制创建b表，但是a表的索引等却复制不了，需要在b中手动建立。

5. insert into 会将查询结果保存到已经存在的表中   
```insert into t2(column1, column2, ....) select column1, column2, .... from t1```
