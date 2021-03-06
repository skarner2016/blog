---
title: MySQL规范
date: 2022-07-13 11:27:12
tags: 
- MySQL
- standard
categories: 
- MySQL
---

#### 1.命名规范

1.1 库名、表名、字段必须使用小写，以下划线分隔，需见名知意
1.2 一般不超过32个字符，不使用MySQL保留字
1.3 临时库、表，必须以tmp为前缀，以日期为后缀
1.4 备份库、表，必须以bak为前缀，以日期为后缀
1.5 使用utf8mb4字符集，一般使用 utf8mb4_general_ci(5.7)/utf8mb4_0900_ai_ci（8.0） 为字符集


#### 2.设计规范

2.1 所有表必须有主键，并以id命名，不使用uuid做索引，建议使用自增ID或发号器
2.2 时间、日期统一使用 datetime(YYYY-MM-DD HH:II:SS)
2.3 拆分大字段、访问频率低的字段，分离冷热数据
2.4 禁止使用分区表
2.5 字段不可定义为 NULL
2.6 非必要，不分表（一般表3年数据量低于千万级，无需分表，日志、操作记录类表，根据增量按年、月、周分表）
2.7 浮点数用 decimal 存储
2.8 不可使用枚举字段，用UNSIGNED TINYINT/UNSIGNED INT替代，并备注各自含义
2.9 数据库中不允许存储大文件、图片，存储到OSS中
2.10 ip地址存储INT,而非CHAR
2.11 禁止使用外键
2.12 敏感数据禁止明文存储，如密码



#### 3.索引规范

3.1 索引数量不可过多，单张表不超过5个
3.2 单个索引中字段不可超过5个
3.3 索引建议
3.3.1 常用的WHERE条件的字段
3.3.2 常用的ORDER BY字段
3.3.3 常用的GROUP BY字段
3.3.4 常用的DISTINCT字段
3.3.5 索引的选择性值低的字段(20%)，不建议建立索引，如性别
3.4 索引命名，主键pk_，唯一索引uk_, 普通索引idx_

#### 4.SQL规范

4.1 复杂SQL，尽可能拆成小的、简单的SQL
4.2 尽量避免使用触发器、函数、存储过程
4.3 尽量避免在数据库中进行数学运算
4.4 尽量用 IN() 代替 OR
4.5 IN 中元素的个数尽量少于500个
4.6 尽量避免使用JOIN
4.7 禁止使用 ORDER BY RAND()
