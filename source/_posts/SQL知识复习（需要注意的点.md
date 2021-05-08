---
title: SQL知识复习（需要注意的点
author: 汉娜
tags: SQL知识点
categories: 数据库
date: 2021-05-07 15:52:07
---


#### SELECT DISTINCT 语句用于返回唯一不同的值。


#### ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，可以使用 DESC 关键字。


#### SQL INSERT INTO 语法有两种编写形式。
第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：
```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```
第二种形式需要指定列名及被插入的值：
```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```


#### SQL SELECT TOP, LIMIT, ROWNUM 子句
SQL Server / MS Access 语法：
```
SELECT TOP number|percent column_name(s)
FROM table_name;
```
MySQL 语法：
```
SELECT column_name(s)
FROM table_name
LIMIT number;
```
Oracle 语法：
```
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
```


#### SQL 通配符
_ 通配符：替代一个字符
REGEXP/NOT REGEXP/RLIKE/NOT RLIKE '^ [charlist]'：字符列中的任何单一字符
```
SELECT * FROM Websites
WHERE name REGEXP '^[A-H]';
```
REGEXP/NOT REGEXP/RLIKE/NOT RLIKE '^ [^charlist]'：不在字符列中的任何单一字符
```
SELECT * FROM Websites
WHERE name REGEXP '^[^A-H]';
```


#### CONCAT（）把多列结合在一起
在下面的 SQL 语句中，把三个列（url、alexa 和 country）结合在一起，并创建一个名为 "site_info" 的别名
```
SELECT name, CONCAT(url, ', ', alexa, ', ', country) AS site_info
FROM Websites;
```


#### JOIN连接
![7种join](/images/sql_join.png)
1. INNER JOIN ON（INNER JOIN 与 JOIN 是相同的）
```
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;
```
或
```
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```
2. LEFT JOIN ON（在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN）
从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。
```
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;
```
或
```
SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```
3.RIGHT JOIN ON（在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN）
从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。
```
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name=table2.column_name;
```
或
```
SELECT column_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```
4.FULL OUTER JOIN ON（mysql不支持，SQL Server支持 ）
只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行。
结合了 LEFT JOIN 和 RIGHT JOIN 的结果。
```
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name=table2.column_name;
```


#### UNION
合并两个或多个 SELECT 语句的结果，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。
```
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```
UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。
```
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```


#### SELECT INTO（MySQL 数据库不支持 SELECT ... INTO 语句，但支持 INSERT INTO ... SELECT）
从一个表复制数据，然后把数据插入到另一个新表中。
```
SELECT *
INTO newtable [IN externaldb]
FROM table1;
```
或者只复制希望的列插入到新表中：
```
SELECT column_name(s)
INTO newtable [IN externaldb]
FROM table1;
```
或者拷贝表结构及数据：
```
CREATE TABLE 新表
AS
SELECT * FROM 旧表 
```


#### INSERT INTO SELECT
从一个表复制数据，然后把数据插入到一个已存在的表中。
```
INSERT INTO table2
SELECT * FROM table1;
```
或者只复制希望的列插入到另一个已存在的表中：
```
INSERT INTO table2
(column_name(s))
SELECT column_name(s)
FROM table1;
```


#### SQL约束
1.NOT NULL
```
ALTER TABLE Persons MODIFY Age int NOT NULL;
ALTER TABLE Persons MODIFY Age int NULL;
```
2.UNIQUE
```
ALTER TABLE Persons ADD UNIQUE (P_Id);
ALTER TABLE Persons ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName);
ALTER TABLE Persons DROP INDEX uc_PersonID;
ALTER TABLE Persons DROP CONSTRAINT uc_PersonID;
```
3.PRIMARY KEY
```
ALTER TABLE Persons ADD PRIMARY KEY (P_Id);
ALTER TABLE Persons ADD CONSTRAINT pk_PersonID PRIMARY KEY (P_Id,LastName);
ALTER TABLE Persons DROP PRIMARY KEY;
ALTER TABLE Persons DROP CONSTRAINT pk_PersonID;
```
4.FOREIGN KEY，指向另一个表中的 UNIQUE KEY
```
ALTER TABLE Orders ADD FOREIGN KEY (P_Id) REFERENCES Persons(P_Id);
ALTER TABLE Orders ADD CONSTRAINT fk_PerOrders FOREIGN KEY (P_Id) REFERENCES Persons(P_Id);
ALTER TABLE Orders DROP FOREIGN KEY fk_PerOrders;
ALTER TABLE Orders DROP CONSTRAINT fk_PerOrders;
```
5.CHECK
```
ALTER TABLE Persons ADD CHECK (P_Id>0);
ALTER TABLE Persons ADD CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes');
ALTER TABLE Persons DROP CONSTRAINT chk_Person;
ALTER TABLE Persons DROP CHECK chk_Person;
```
6.DEFAULT
```
ALTER TABLE Persons ALTER City SET DEFAULT 'SANDNES';
ALTER TABLE Persons ADD CONSTRAINT ab_c DEFAULT 'SANDNES' for City;
ALTER TABLE Persons MODIFY City DEFAULT 'SANDNES';
ALTER TABLE Persons ALTER City DROP DEFAULT;
ALTER TABLE Persons ALTER COLUMN City DROP DEFAULT;
```


#### DROP删除表结构，TRUNCATE删除表内容，空间恢复到初始大小，而DELETE不会减少表或索引所占的空间
```
DROP TABLE table_name;
TRUNCATE TABLE table_name;
```


#### NULL值赋为0
```
SELECT ProductName,UnitPrice*(UnitsInStock+ISNULL(UnitsOnOrder,0)) FROM Products;
SELECT ProductName,UnitPrice*(UnitsInStock+NVL(UnitsOnOrder,0)) FROM Products;
SELECT ProductName,UnitPrice*(UnitsInStock+IFNULL(UnitsOnOrder,0)) FROM Products;
SELECT ProductName,UnitPrice*(UnitsInStock+COALESCE(UnitsOnOrder,0)) FROM Products;
```

