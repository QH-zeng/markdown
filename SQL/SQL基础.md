# SQL

https://www.w3school.com.cn/sql/sql_notnull.asp

## ——初级SQL——

SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

查询和更新指令构成了 SQL 的 DML 部分：

- *SELECT* - 从数据库表中获取数据
- *UPDATE* - 更新数据库表中的数据
- *DELETE* - 从数据库表中删除数据
- *INSERT INTO* - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

SQL 中最重要的 DDL 语句:

- *CREATE DATABASE* - 创建新数据库
- *ALTER DATABASE* - 修改数据库
- *CREATE TABLE* - 创建新表
- *ALTER TABLE* - 变更（改变）数据库表
- *DROP TABLE* - 删除表
- *CREATE INDEX* - 创建索引（搜索键）
- *DROP INDEX* - 删除索引

## "Persons" 表:

|  Id  | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

## "Orders" 表：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

## ——例子表格——



## SELECT语句

**语法：**

```sql
SELECT 列名 FROM 表名
SELECT *    FROM 表名  查询所有列
```



## SELECT DISTINCT语句

在表中，可能会包含重复值。希望仅仅列出不同（distinct）的值。关键词 DISTINCT 用于返回唯一不同的值。

**语法：**

```sql
SELECT DISTINCT 列名称 FROM 表名称
```



## WHERE 子句

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。

**语法：**

```sql
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```

------------------------------

| 操作符  | 描述         |
| :------ | :----------- |
| =       | 等于         |
| <>      | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |

SQL 使用**单引号**来环绕***文本值***（大部分数据库系统也接受双引号）。如果是***数值***，**不使用引号**。

example：

文本值：

```sql
这是正确的：
SELECT * FROM Persons WHERE FirstName='Bush'

这是错误的：
SELECT * FROM Persons WHERE FirstName=Bush
```

数值：

```sql
这是正确的：
SELECT * FROM Persons WHERE Year>1965

这是错误的：
SELECT * FROM Persons WHERE Year>'1965'
```



## AND 和 OR 运算符

AND 和 OR 可在 **WHERE 子语句**中把两个或多个条件结合起来。

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

example：

```sql
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'

SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'
```

## ORDER BY 语句

**ORDER BY 语句用于对结果集进行排序。**

**DESC是descend 降序意思**
**ASC是ascend 升序意思**

ORDER BY 语句用于根据指定的列对结果集进行排序。

ORDER BY 语句**默认按照升序（默认ASC）**对记录进行排序。

如果您希望按照降序对记录进行排序，可以使用 DESC 关键字。

example：

```sql
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC
```



## INSERT INTO 语句

INSERT INTO 语句用于向表格中插入新的行。

**语法：**

```sql
INSERT INTO 表名称 VALUES (值1, 值2,....)
```

我们也可以指定所要插入数据的列：**没有指定的就为null**

```sql
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```

"Persons" 表：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |

example：

```sql
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
```

```sql
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```

## UPDATE语句

Update 语句用于修改表中的数据。

**语法：**

```sql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```

example

**更新某一行中的一个列：**我们为 lastname 是 "Wilson" 的人添加 firstname：

```sql
UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson' 
```

**更新某一行中的若干列：**我们会修改地址（address），并添加城市名称（city）：

```sql
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson'
```

## DELETE 语句

DELETE 语句用于删除表中的行。

**语法：**

```sql
DELETE FROM 表名称 WHERE 列名称 = 值
```

example:

**删除某行:**"Fred Wilson" 会被删除：

```sql
DELETE FROM Person WHERE LastName = 'Wilson' 
```

**删除所有行:**可以在不删除表的情况下删除所有的行。这意味着表的结构、属性和索引都是完整的：

```sql
DELETE FROM table_name
DELETE * FROM table_name
```

------



## ——高级SQL——



## TOP 子句

TOP 子句用于规定要返回的记录的数目。

对于拥有数千条记录的大型表来说，TOP 子句是非常有用的。

**注释：**并非所有的数据库系统都支持 TOP 子句。

SQL Server 的**语法：**

```sql
SELECT TOP number|percent column_name(s)
FROM table_name
```

**MySQL 语法**

```sql
SELECT column_name(s)
FROM table_name
LIMIT number
```

example

```sql
SELECT *
FROM Persons
LIMIT 5
```

Oracle 语法

```sql
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number
```

## LIKE 操作符

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

SQL LIKE 操作符语法

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern
```

example

从 "Persons" 表中选取居住在以 "N" 开始的城市里的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City LIKE 'N%'
```

从 "Persons" 表中选取居住在以 "g" 结尾的城市里的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City LIKE '%g'
```

从 "Persons" 表中选取居住在包含 "lon" 的城市里的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City LIKE '%lon%'
```

通过使用 NOT 关键字，从 "Persons" 表中选取居住在*不包含* "lon" 的城市里的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City NOT LIKE '%lon%'
```

## SQL 通配符

在搜索数据库中的数据时，SQL 通配符可以替代一个或多个字符。

SQL 通配符必须与 LIKE 运算符一起使用。

在 SQL 中，可使用以下通配符：

| 通配符                     | 描述                       |
| :------------------------- | :------------------------- |
| %                          | 替代**一个或多个字符**     |
| _                          | **仅替代一个字符**         |
| [charlist]                 | 字符列中的任何**单一字符** |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

example

使用 [charlist] 通配符:从上面的 "Persons" 表中选取居住的城市以 "A" 或 "L" 或 "N" 开头的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City LIKE '[ALN]%'
```

从上面的 "Persons" 表中选取居住的城市*不以* "A" 或 "L" 或 "N" 开头的人：可以使用下面的 SELECT 语句：

```sql
SELECT * FROM Persons
WHERE City LIKE '[!ALN]%'
```

## IN 操作符

IN 操作符允许我们在 WHERE 子句中**规定某一列多个值。**

注意与and/or区分

and:同时满足两个条件

or：满图两个条件其中一个

**SQL IN 语法**

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...)
```

example

```sql
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')
```

## BETWEEN 操作符

操作符 **BETWEEN ... AND** 会选取介于两个值之间的数据范围。这些值可以是数值、文本或者日期。

**BETWEEN 操作符在 WHERE 子句中使用，作用是选取介于两个值之间的数据范围。**

**SQL BETWEEN 语法**

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name
BETWEEN value1 AND value2
/ NOT BETWEEN  AND
```

example

如需以字母顺序显示介于 "Adams"（包括）和 "Carter"（不包括）之间的人，请使用下面的 SQL：

```sql
SELECT * FROM Persons
WHERE LastName
BETWEEN 'Adams' AND 'Carter'
```

**提示：**

不同的数据库对 BETWEEN...AND 操作符的处理方式是有差异的。

某些数据库会列出介于 "Adams" 和 "Carter" 之间的人，**但不包括 "Adams" 和 "Carter" ；**

某些数据库会列出介于 "Adams" 和 "Carter" 之间**并包括 "Adams" 和 "Carter" 的人——MYSQL属于这一种**

一些数据库会列出介于 "Adams" 和 "Carter" 之间的人，**包括 "Adams" ，但不包括 "Carter" 。**



## SQL Alias 别名

**通过使用 SQL，可以为列名称和表名称指定别名（Alias）。**

表的 SQL Alias 语法

```SQL
SELECT column_name(s)
FROM table_name
AS alias_name
```

列的 SQL Alias 语法

```SQL
SELECT column_name AS alias_name
FROM table_name
```

Alias 实例: 使用表名称别名---------------别名使查询程序更易阅读和书写。

假设我们有两个表分别是："Persons" 和 "Product_Orders"。我们分别为它们指定别名 "p" 和 "po"。

现在，我们希望列出 "John Adams" 的所有定单。

我们可以使用下面的 SELECT 语句：

```SQL
SELECT po.OrderID, p.LastName, p.FirstName
FROM Persons AS p, Product_Orders AS po
WHERE p.LastName='Adams' AND p.FirstName='John'
```

不使用别名的 SELECT 语句：

```SQL
SELECT Product_Orders.OrderID, Persons.LastName, Persons.FirstName
FROM Persons, Product_Orders
WHERE Persons.LastName='Adams' AND Persons.FirstName='John'
```

## SQL UNION 操作符

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

**SQL UNION 语法**

```sql
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```

**SQL UNION ALL 语法**

```sql
SELECT column_name(s) FROM table_name1
UNION ALL
SELECT column_name(s) FROM table_name2
```

**注释：**默认地，UNION 操作符只会选取不同的值。UNION ALL允许重复的值，全部查询出来。

​	UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。





## SELECT INTO 语句

**SQL SELECT INTO 语句可用于创建表的备份复件。**

SELECT INTO 语句从一个表中选取数据，然后把数据插入另一个表中。

SELECT INTO 语句常用于创建表的备份复件或者用于对记录进行存档。

**SQL SELECT INTO 语法**

把所有的列插入新表：

```sql
SELECT *
INTO new_table_name [IN externaldatabase] 
FROM old_tablename
```

只把希望的列插入新表：

```sql
SELECT column_name(s)
INTO new_table_name [IN externaldatabase] 
FROM old_tablename
```



## ——SQL JOIN查询——

**SQL join 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。**

### Join 和 Key

有时为了得到完整的结果，我们需要从两个或更多的表中获取结果。我们就需要执行 join。

数据库中的表可通过键将彼此联系起来。主键（Primary Key）是一个列，在这个列中的每一行的值都是唯一的。在表中，每个主键的值都是唯一的。这样做的目的是在不重复每个表中的所有数据的情况下，把表间的数据交叉捆绑在一起。

### 方法一：多表查询——隐式内连接，用Where消除无用数据

"Persons" 表:

|  Id  | LastName | FirstName |    Address     |   City   |
| :--: | :------: | :-------: | :------------: | :------: |
|  1   |  Adams   |   John    | Oxford Street  |  London  |
|  2   |   Bush   |  George   |  Fifth Avenue  | New York |
|  3   |  Carter  |  Thomas   | Changan Street | Beijing  |

"Orders" 表：

| Id_O | OrderNo | Id_P |
| :--: | :-----: | :--: |
|  1   |  77895  |  3   |
|  2   |  44678  |  3   |
|  3   |  22456  |  1   |
|  4   |  24562  |  1   |
|  5   |  34764  |  65  |

从两个表分别查询需要的信息



```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons, Orders
WHERE Persons.Id_P = Orders.Id_P 
```

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

### 方法二：SQL JOIN - 使用 Join

除了上面的方法，我们也可以使用关键词 JOIN 来从两个表中获取数据。

example

如果我们希望列出所有人的定购，可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P = Orders.Id_P
ORDER BY Persons.LastName
```

### 不同的 SQL JOIN

除了我们在上面的例子中使用的 INNER JOIN（内连接），我们还可以使用其他几种连接。

下面列出了您可以使用的 JOIN 类型，以及它们之间的差异。

- JOIN: 如果表中有至少一个匹配，则返回行
- LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行
- RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行
- FULL JOIN: 只要其中一个表中存在匹配，就返回行

## SQL INNER JOIN （内连接）

在表中**存在至少一个匹配时**，INNER JOIN 关键字返回行。

**INNER JOIN 关键字语法**

```sql
SELECT column_name(s)——字段列表
FROM table_name1——表名1
[INNER] JOIN table_name2——表名2  inner可选
ON table_name1.column_name=table_name2.column_name  ——条件
```

**注释：**INNER JOIN 与 JOIN 是相同的。

example

列出所有人的定购。：可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

**INNER JOIN 关键字在表中存在至少一个匹配时返回行。如果 "Persons" 中的行在 "Orders" 中没有匹配，就不会列出这些行。**

## SQL LEFT JOIN （左外连接）

**LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。**

想要查询左表的数据，如果右表没有就显示为空，一起查询出来

如果没有用的left join 的话，右表没有的数据不会被查到

**LEFT JOIN 关键字语法**

```sql
SELECT column_name(s)
FROM table_name1
LEFT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**注释：**在某些数据库中， LEFT JOIN 称为 LEFT OUTER JOIN。

example

列出所有的人，以及他们的定购 - 如果有的话。可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
LEFT JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |

**LEFT JOIN 关键字会从左表 (Persons) 那里返回所有的行，即使在右表 (Orders) 中没有匹配的行。**

## SQL RIGHT JOIN （右外连接）

RIGHT JOIN 关键字会右表 (table_name2) 那里返回所有的行，即使在左表 (table_name1) 中没有匹配的行。

**RIGHT JOIN 关键字语法**

```sql
SELECT column_name(s)
FROM table_name1
RIGHT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**注释：**在某些数据库中， RIGHT JOIN 称为 RIGHT OUTER JOIN。

example

列出所有的定单，以及定购它们的人 - 如果有的话。可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
RIGHT JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
|          |           | 34764   |

**RIGHT JOIN 关键字会从右表 (Orders) 那里返回所有的行，即使在左表 (Persons) 中没有匹配的行。**

## SQL FULL JOIN （全连接）

只要其中某个表存在匹配，FULL JOIN 关键字就会返回行。

**FULL JOIN 关键字语法**

```sql
SELECT column_name(s)
FROM table_name1
FULL JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**注释：**在某些数据库中， FULL JOIN 称为 FULL OUTER JOIN。

example

列出所有的人，以及他们的定单，以及所有的定单，以及定购它们的人。可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
FULL JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

结果集：

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |
|          |           | 34764   |

**FULL JOIN 关键字会从左表 (Persons) 和右表 (Orders) 那里返回所有的行。如果 "Persons" 中的行在表 "Orders" 中没有匹配，或者如果 "Orders" 中的行在表 "Persons" 中没有匹配，这些行同样会列出。**



## 子查询（嵌套查询）

### 子查询的结果是单行单列的

子查询可以作为条件，使用运算符去判断，操作运算符为：<,>,=,>=,<=

```sql
select *  from emp
where emp.salary=(select Max(salary) from emp)
```



### 子查询的结果是单行多列的

子查询可以作为条件，使用操作符in来判断

```sql
select *  from emp
where emp.dept_id in(select id from dept where name=XX or name= XX)
```



### 系查询的结果可以是多行多列的

## ——SQL 约束（Constraints）——

约束用于限制加入表的数据的类型。

可以在**创建表时规定约束**（通过 CREATE TABLE 语句），或者在**表创建之后也可以**（通过 ALTER TABLE 语句）。

我们将主要探讨以下几种约束：

- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT



## SQL NOT NULL 约束

NOT NULL 约束强制列不接受 NULL 值。

NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录

## SQL UNIQUE 约束

UNIQUE 约束唯一标识数据库表中的每条记录。

UNIQUE 和 PRIMARY KEY 约束均为列或列集合提供了唯一性的保证。

PRIMARY KEY 拥有自动定义的 UNIQUE 约束。

请注意，每个表可以有多个 UNIQUE 约束，但是每个表只能有一个 PRIMARY KEY 约束。

```sql
CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (Id_P)
)
```



```sql
ADD UNIQUE (Id_P)  单个
ADD CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)  多个唯一性约束
```

## SQL PRIMARY KEY 约束

PRIMARY KEY 约束唯一标识数据库表中的每条记录。

主键必须包含唯一的值。

主键列不能包含 NULL 值。

每个表都应该有一个主键，并且每个表只能有一个主键。

**表已存在的情况下为 "Id_P" 列创建 PRIMARY KEY 约束**

```sql
ADD PRIMARY KEY (Id_P)
ADD CONSTRAINT pk_PersonID PRIMARY KEY (Id_P,LastName)

撤销约束
DROP PRIMARY KEY
DROP CONSTRAINT pk_PersonID
```



## SQL FOREIGN KEY 约束

一个表中的 FOREIGN KEY 指向另一个表中的 PRIMARY KEY。

```sql
alter table 表名  drop foreign key  外键名字
```



## SQL CHECK 约束

**CHECK 约束用于限制列中的值的范围。**

如果对单个列定义 CHECK 约束，那么该列只允许特定的值。

如果对一个表定义 CHECK 约束，那么此约束会在特定的列中对值进行限制。

**如果需要命名 CHECK 约束，以及为多个列定义 CHECK 约束，请使用下面的 SQL 语法：**

```
CONSTRAINT chk_Person CHECK (Id_P>0 AND City='Sandnes')

在表已存在的情况下为 "Id_P" 列创建 CHECK 约束，请使用下面的 SQL：
ADD CHECK (Id_P>0)
ADD CONSTRAINT chk_Person CHECK (Id_P>0 AND City='Sandnes')

DROP CONSTRAINT chk_Person
DROP CHECK chk_Person
```



## SQL DEFAULT 约束

DEFAULT 约束用于向列中插入默认值。

如果没有规定其他的值，那么会将默认值添加到所有的新记录。

```sql
ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES'

ALTER TABLE Persons
ALTER City DROP DEFAULT
```



## 索引

您可以在表中创建索引，以便更加快速高效地查询数据。

用户无法看到索引，它们只能被用来加速搜索/查询。

**注释：**更新一个包含索引的表需要比更新一个没有索引的表更多的时间，这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被搜索的列（以及表）上面创建索引。

**在不读取整个表的情况下，索引使数据库应用程序可以更快地查找数据。**







# SQL Date 函数

## SQL 日期

当我们处理日期时，最难的任务恐怕是确保所插入的日期的格式，与数据库中日期列的格式相匹配。

只要数据包含的只是日期部分，运行查询就不会出问题。但是，如果涉及时间，情况就有点复杂了。

在讨论日期查询的复杂性之前，我们先来看看最重要的内建日期处理函数。

## MySQL Date 函数

下面的表格列出了 MySQL 中最重要的内建日期函数：

| 函数                                                         | 描述                                |
| :----------------------------------------------------------- | :---------------------------------- |
| [NOW()](https://www.w3school.com.cn/sql/func_now.asp)        | 返回当前的日期和时间                |
| [CURDATE()](https://www.w3school.com.cn/sql/func_curdate.asp) | 返回当前的日期                      |
| [CURTIME()](https://www.w3school.com.cn/sql/func_curtime.asp) | 返回当前的时间                      |
| [DATE()](https://www.w3school.com.cn/sql/func_date.asp)      | 提取日期或日期/时间表达式的日期部分 |
| [EXTRACT()](https://www.w3school.com.cn/sql/func_extract.asp) | 返回日期/时间按的单独部分           |
| [DATE_ADD()](https://www.w3school.com.cn/sql/func_date_add.asp) | 给日期添加指定的时间间隔            |
| [DATE_SUB()](https://www.w3school.com.cn/sql/func_date_sub.asp) | 从日期减去指定的时间间隔            |
| [DATEDIFF()](https://www.w3school.com.cn/sql/func_datediff_mysql.asp) | 返回两个日期之间的天数              |
| [DATE_FORMAT()](https://www.w3school.com.cn/sql/func_date_format.asp) | 用不同的格式显示日期/时间           |

## SQL Date 数据类型

MySQL 使用下列数据类型在数据库中存储日期或日期/时间值：

- DATE - 格式 YYYY-MM-DD
- DATETIME - 格式: YYYY-MM-DD HH:MM:SS
- TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS
- YEAR - 格式 YYYY 或 YY

## MySQL 数据类型

在 MySQL 中，有三种主要的类型：文本、数字和日期/时间类型。

### Text 类型：

| 数据类型         | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| CHAR(size)       | 保存固定长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的长度。最多 255 个字符。 |
| VARCHAR(size)    | 保存可变长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的最大长度。最多 255 个字符。注释：如果值的长度大于 255，则被转换为 TEXT 类型。 |
| TINYTEXT         | 存放最大长度为 255 个字符的字符串。                          |
| TEXT             | 存放最大长度为 65,535 个字符的字符串。                       |
| BLOB             | 用于 BLOBs (Binary Large OBjects)。存放最多 65,535 字节的数据。 |
| MEDIUMTEXT       | 存放最大长度为 16,777,215 个字符的字符串。                   |
| MEDIUMBLOB       | 用于 BLOBs (Binary Large OBjects)。存放最多 16,777,215 字节的数据。 |
| LONGTEXT         | 存放最大长度为 4,294,967,295 个字符的字符串。                |
| LONGBLOB         | 用于 BLOBs (Binary Large OBjects)。存放最多 4,294,967,295 字节的数据。 |
| ENUM(x,y,z,etc.) | 允许你输入可能值的列表。可以在 ENUM 列表中列出最大 65535 个值。如果列表中不存在插入的值，则插入空值。注释：这些值是按照你输入的顺序存储的。可以按照此格式输入可能的值：ENUM('X','Y','Z') |
| SET              | 与 ENUM 类似，SET 最多只能包含 64 个列表项，不过 SET 可存储一个以上的值。 |

### Number 类型：

| 数据类型        | 描述                                                         |
| :-------------- | :----------------------------------------------------------- |
| TINYINT(size)   | -128 到 127 常规。0 到 255 无符号*。在括号中规定最大位数。   |
| SMALLINT(size)  | -32768 到 32767 常规。0 到 65535 无符号*。在括号中规定最大位数。 |
| MEDIUMINT(size) | -8388608 到 8388607 普通。0 to 16777215 无符号*。在括号中规定最大位数。 |
| INT(size)       | -2147483648 到 2147483647 常规。0 到 4294967295 无符号*。在括号中规定最大位数。 |
| BIGINT(size)    | -9223372036854775808 到 9223372036854775807 常规。0 到 18446744073709551615 无符号*。在括号中规定最大位数。 |
| FLOAT(size,d)   | 带有浮动小数点的小数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DOUBLE(size,d)  | 带有浮动小数点的大数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。 |
| DECIMAL(size,d) | 作为字符串存储的 DOUBLE 类型，允许固定的小数点。             |

\* 这些整数类型拥有额外的选项 UNSIGNED。通常，整数可以是负数或正数。如果添加 UNSIGNED 属性，那么范围将从 0 开始，而不是某个负数。

### Date 类型：

| 数据类型    | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| DATE()      | 日期。格式：YYYY-MM-DD注释：支持的范围是从 '1000-01-01' 到 '9999-12-31' |
| DATETIME()  | *日期和时间的组合。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59' |
| TIMESTAMP() | *时间戳。TIMESTAMP 值使用 Unix 纪元('1970-01-01 00:00:00' UTC) 至今的描述来存储。格式：YYYY-MM-DD HH:MM:SS注释：支持的范围是从 '1970-01-01 00:00:01' UTC 到 '2038-01-09 03:14:07' UTC |
| TIME()      | 时间。格式：HH:MM:SS 注释：支持的范围是从 '-838:59:59' 到 '838:59:59' |
| YEAR()      | 2 位或 4 位格式的年。注释：4 位格式所允许的值：1901 到 2155。2 位格式所允许的值：70 到 69，表示从 1970 到 2069。 |

\* 即便 DATETIME 和 TIMESTAMP 返回相同的格式，它们的工作方式很不同。在 INSERT 或 UPDATE 查询中，TIMESTAMP 自动把自身设置为当前的日期和时间。TIMESTAMP 也接受不同的格式，比如 YYYYMMDDHHMMSS、YYMMDDHHMMSS、YYYYMMDD 或 YYMMDD。



# SQL 函数

函数大全http://c.biancheng.net/mysql/function/

## 函数的语法

内建 SQL 函数的语法是：

```
SELECT function(列) FROM 表
```

## 函数的类型

在 SQL 中，基本的函数类型和种类有若干种。函数的基本类型是：

- Aggregate 函数
- Scalar 函数



## GROUP BY 语句

GROUP BY 语句用于结合合计函数，根据一个或多个列对结果集进行分组。

### SQL GROUP BY 语法

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
```

## HAVING 子句

在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与合计函数一起使用。

### SQL HAVING 语法

```
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value
```







