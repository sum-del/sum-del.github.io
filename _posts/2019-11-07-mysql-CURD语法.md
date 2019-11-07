---
layout: post
title: 'Mysql-CURD'
date: 2019-11-06
categories: test
tags: mysql
---

MySQL最基本的几个操作就是:  增删改查

技术名词 **CURD**:  创建（Create）、更新（Update）、读取（Retrive）和删除（Delete）

## 增

主要用于数据库**添加数据**

**格式1**:   

添加一条 **完整**的数据 (包含所有的字段)

```
INSERT INTO `表名`  VALUES("值1", "值2", ... )
```



**格式2:**

添加一条 **指定部分字段** 的数据

```
INSERT INTO `表名`(`字段名1`, `字段名2`, ...) VALUES("值1", "值2", ...)
```



**格式3:**

添加**多条** **完整**的数据

```
INSERT INTO `表名`  VALUES("值1", "值2", ... ), ("值1", "值2", ... ), ...
```



**格式4:**

添加**多条** **指定部分字段**的数据

```
INSERT INTO `表名`(`字段名1`, `字段名2`, ...) VALUES("值1", "值2", ...), ("值1", "值2", ...), ...
```



**注意:**

1. **添加部分字段时**
   - 具有 **not null** 属性的字段, **必须添加**
   - **值** 的**书写顺序**, 必须按照 前面**字段名的顺序**,  一 一对应

2. **添加完整字段时**
   - 带有 **auto_increment** 属性的字段, 可不指定值, 可用**null**代替.  例如 "主键"
   - 带有 **default** 属性的字段, 可不指定值, 可用 **default** 调用**默认值**
3. 带有 **unique** 的字段, 添加时要 **避免重复**, 否则会报错



## 删

主要用于**删除**数据库**某一条**, **多条** 或 **全部数据**, **不会影响表结构**

**格式1:**

删除**一张表**的**所有数据**

```
DELETE FROM `表名`
```



**格式2:**

删除一张表中 **满足条件**的数据

```
DELETE FROM `表名` WHERE 条件
```



**格式3:**

删除一张表中 按照**排序**的  **前几条 **[满足条件] 数据.

格式中 **[ ]** 代表的where**可写可不写**

```
DELETE FROM `表名` [WHERE 条件] ORDER BY 排序依据 LIMIT 行数
```



**注意:**

1. **delete** 只会删除表数据, **drop** 会删除表结构   (结构没了, 数据自然也无容身之地) 
2. 推荐在 delete 或 drop 之前,  做好**数据备份**
3. 若删除大批量数据的话, 建议使用 `truncate table 表名`

```
truncate table `表名`

该写法, 会直接重构表结构, 清除数据, auto_increment 也重置为1
```





## 备份

1. 按 `win + R` 进入运行框
2. 输入 `cmd` 进入 命令提示符
3. 输入 `mysqldump -u 用户名 -p 数据库名 > 目标地址` 来备份

```
例如:  mysqldump -u root -p `user` > D:/a.sql
	  将 `user` 库备份到 D盘下, 存储为 a.sql 文件
```

**注意:**

​	1. 备份命令的**最后不要加分号**

> 友情提醒: 
>
> ​	mysql 备份 或 导入, 是不需要进入MySQL环境的,  直接在cmd环境中就可以操作

## 导入

1. 按 `win + R` 进入运行框
2. 输入 `cmd` 进入 命令提示符
3. 输入 `mysql -u 用户名 -p 数据库名 < 来源地址` 来导入

```
例如: mysql -u root -p `user` < D:/a.sql
	 从 D盘下 a.sql 文件导入到 `user` 库中
```

**注意:**

导入前, 需要确保两件事情,  来源sql文件的**最前面**是否有 `建库` 和 `用库` 代码, 否则导入可能会失败.

因为不少备份sql文件, 只备份结构和数据, 而没有备份库, 所有需要在 备份sql文件的最前面补上 建库和用库的代码.



## 改

主要用于**修改**表中的一条, 多条 或 全部数据

**格式1:**

将 一张表中 **所有** 符合 字段名1和字段名2 的**都修改**了

```
UPDATE `表名` SET `字段名1`='值1', `字段名2`='值2', ...
```

**格式2:**

将一张表中 **所有符合条件**的字段名 **都修改**了

```
UPDATE `表名` SET `字段名1`='值1', `字段名2`='值2', ... WHERE 条件
```



**注意:**

1. 不带 **where** 条件, 会对整张表进行修改
2. 带 **where** 条件, 仅对局部数据进行修改



## 查

主要用于 **查询** 数据表中的 数据

**完整语句格式**

```
SELECT [ALL|DISTINCT] [*|字段名|表名.字段名|表名.字段名 as 别名|字段名 as 别名|函数| ... ]
[FROM 表名|表名1,表名2, ... ]
[WHERE 条件]
[GROUP BY 分组依据]
[HAVING 聚合函数]
[ORDER BY 排序依据][ASC|DESC]
[LIMIT 偏移量 [,条数] ]
```



### 常用函数

**查询当前时间**

时间格式:  YYYY-MM-DD HH:MM:SS

```
SELECT NOW()
```

**查询当前时间戳**

```
SELECT UNIX_TIMESTAMP()
```

**查询当前MySQL版本**

```
SELECT VERSION()
```

**查询md5加密**

```
SELECT MD5('字符串')
```

**查询运算结果**

```
SELECT 10 + 20
```







### 基本查询

**查询一张表中 所有数据**

```
SELECT * FROM 表名
```

**注意:** 

1.  `*`  是通配符,  代表能匹配所有的字段
2.  `*`  将需要的 和 不需要的都匹配出来了,  有时会浪费mysql的性能, 所以 慎用

**查询一张表中  部分字段数据**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名`
```

**查询一张表中,  字段名A一共有多少条数据**

```
SELECT count(`字段名A`) FROM `表名`
```

**查询一张表中,  字段名A的总和**

```
SELECT sum(`字段名A`) FROM `表名`
```

**查询一张表中,  字段名A的平均值**

```
SELECT avg(`字段名A`) FROM `表名`
```

**查询一张表中,  字段名A中的最大值**

```
SELECT max(`字段名A`) FROM `表名`
```

**查询一张表中,  字段名A中的最小值**

```
SELECT min(`字段名A`) FROM `表名`
```

**查询数据,  按照指定格式进行展示**

```
SELECT  concat( s1,s2,s3, ...  ) FROM `表名`
```

这里的s1, s2, s3 可以是字段名, 也可以是 任意普通字符串

concat 具有将 s1, s2, s3 拼接起来的效果



**查询一张表中  满足条件的 部分字段数据**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` WHERE 条件
```

**按指定条件 分组查询信息**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` [WHERE 条件] GROUP BY 条件
```

**先按指定条件分组, 再筛选查询**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` [WHERE 条件] GROUP BY 条件 HAVING 筛选条件
```

**按照指定条件排序查询**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` [WHERE 条件] [GROUP BY 条件 HAVING 筛选条件] ORDER BY 条件 排序方式
```

排序方式:

- asc 升序, 默认
- desc 降序

**提取结果集中, 从第一条开始, 向后连续n条的数据**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` [...] LIMIT n
```

**提取结果集中, 从第m条开始, 向后连续n条的数据**

```
SELECT `字段名1`,`字段名2`, ... FROM `表名` [...] LIMIT m,n
```

- m 可以理解为是结果集中的下标or偏移量.

- m 最小为0, 是结果集中的第一条数据

- 后期常被用于 数据分页



**别名**

```
SELECT `字段名1` AS 别名1, `字段名2` AS 别名2, ... FROM `表名` AS 别名3
```

* 这是的别名可以用于 字段, 也可以用于 表名
* AS 可以省略



**取消重复数据**

```
SELECT DISTINCT`字段名1`, `字段名2` , ... FROM `表名`
```

会将查询到的结果集中, 去掉重复的值



### 常用运算符

#### 算术

```
SELECT 5 + 2
SELECT 5 - 2
SELECT 5 * 2
SELECT 5 / 2  		商为整数, 也可能为小数
SELECT 5 % 2 		模有正有负
SELECT 5 DIV 2  	整除留商
SELECT 5 MOD 2      只取正的模
```

#### 比较

查询user表中,  所有age=18的name

```
SELECT name FROM user WHERE age = 18
```

```
SELECT name FROM user WHERE age < 18
```

```
SELECT name FROM user WHERE age <= 18
```

```
SELECT name FROM user WHERE age > 18
```
```
SELECT name FROM user WHERE age >= 18
```
查询user表中,  所有age 不等于 18的name

```
SELECT name FROM user WHERE age != 18
SELECT name FROM user WHERE age <> 18
```

查询user表中,  所有age 在18 ~ 30 之间的name ( 包含18 和 30)

```
SELECT name FROM user WHERE age BETWEEN 18 AND 30
```

```
SELECT name FROM user WHERE age NOT BETWEEN 18 AND 30
```

查询user表中, 所有 address 是 "北上广" 其中之一的name

```
SELECT name FROM user WHERE address IN (北京,上海,广州)
```

```
SELECT name FROM user WHERE address NOT IN (北京,上海,广州)
```

查询user表中, 所有 email 为空的 name

```
SELECT name FROM user WHERE email IS NULL
```

```
SELECT name FROM user WHERE email IS NOT NULL
```

查询user表中, 所有 name 包含张的 name

```
SELECT name FROM user WHERE name LIKE "%张%"
SELECT name FROM user WHERE name NOT LIKE "张%"
```

- % 可代表多个任意字符
- _ 可代表一个任意字符

#### 逻辑

| 逻辑运算符 | 作用     |
| ---------- | -------- |
| AND        | 逻辑与   |
| OR         | 逻辑或   |
| NOT 或 !   | 逻辑非   |
| XOR        | 逻辑异或 |



> 更高级的select查询:  嵌套查询,  多表联查