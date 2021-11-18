# SQL基础

##### SQL （ Structured Query Language）是什么？

SQL 指**结构化查询语言**

##### SQL 能做什么？

面向数据库：

* 查询
* 取回数据
* 插入新的记录
* 更新数据库中的数据
* 删除记录
* 创建新数据库
* 创建新表
* 创建存储过程
* 创建视图
* 设置表、存储过程和视图的权限

SQL 对大小写不敏感：SELECT 与 select 是相同的。

##### 数据库表

一个数据库通常包含一个或多个表。每个表有一个名字标识，表包含带有数据的记录（行）。



### 重要的 SQL 命令

* SELECT - 从数据库中提取数据
* UPDATE - 更新数据库中的数据
* DELETE - 从数据库中删除数据
* INSERT INTO - 向数据库中插入新数据
* CREATE DATABASE - 创建新数据库
* ALTER DATABASE - 修改数据库
* CREATE TABLE - 创建新表
* ALTER TABLE - 变更（改变）数据库表
* DROP TABLE - 删除表
* CREATE INDEX - 创建索引（搜索键）
* DROP INDEX - 删除索引



where

用于提取那些满足指定条件的记录。

ORDER BY

用于对结果集按照一个列或者多个列进行排序。

`ORDER BY 列名 DESC;`倒序排列

***

## MySQL

##### 常见命令

1. 查看当前所有数据库

   show databases;

2. 打开指定库

   use 库名;

3. 查看当前库的所有表

   show tables;

4. 查看其他库的所有表

   show tables form 库名;

5. 创建表

   create table 表名(

   ​	列名 列类型,

   ​	列名 列类型

   );

6. 查看表结构

   desc 表名;



#### 基础查询

~~~sql
/*
语法：
select 查询列表 from 表名

查询列表可以是：
1.表中的字段
	1.单个
		select 字段 from 表名;
	2.多个，中间逗号隔开
	3.所有字段
		select * from 表名;
2.常量值
3.表达式
4.函数
	显示返回值

查询结果是一个虚拟的表格
*/
-- 1.表中的字段
	-- 1.单个
		select 字段 from 表名;
	-- 2.多个，中间逗号隔开
	-- 3.所有字段
		select * from 表名;
~~~



##### 起别名

`select 字段 as 结果`

> 可以使用` `代替

1. 便于理解
2. 区分重名



##### 去重

关键字`distingct`



##### +

只有运算符功能。

1. 都为数值，直接相加
2. 一个为字符型，试图将字符型转换为数值型
   * 成功——继续做加法，如：'123'-->123
   * 失败——转换为0做加法
3. 一方为null，结果为null