# 概述

数据库按照数据结构来组织、存储和管理数据，实际上，数据库一共有三种模型：

- 层次模型
- 网状模型
- 关系模型

层次模型就是以“上下级”的层次关系来组织数据的一种方式，层次模型的数据结构看起来就像一颗树：

```ascii
            ┌─────┐
            │     │
            └─────┘
               │
       ┌───────┴───────┐
       │               │
    ┌─────┐         ┌─────┐
    │     │         │     │
    └─────┘         └─────┘
       │               │
   ┌───┴───┐       ┌───┴───┐
   │       │       │       │
┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐
│     │ │     │ │     │ │     │
└─────┘ └─────┘ └─────┘ └─────┘
```

网状模型把每个数据节点和其他很多节点都连接起来，它的数据结构看起来就像很多城市之间的路网：

```ascii
     ┌─────┐      ┌─────┐
   ┌─│     │──────│     │──┐
   │ └─────┘      └─────┘  │
   │    │            │     │
   │    └──────┬─────┘     │
   │           │           │
┌─────┐     ┌─────┐     ┌─────┐
│     │─────│     │─────│     │
└─────┘     └─────┘     └─────┘
   │           │           │
   │     ┌─────┴─────┐     │
   │     │           │     │
   │  ┌─────┐     ┌─────┐  │
   └──│     │─────│     │──┘
      └─────┘     └─────┘
```

关系模型把数据看作是一个二维表格，任何数据都可以通过行号+列号来唯一确定，它的数据模型看起来就是一个Excel表：

```ascii
┌─────┬─────┬─────┬─────┬─────┐
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
├─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┘
```

# 数据类型

| 名称         | 类型           | 说明                                                         |
| :----------- | :------------- | :----------------------------------------------------------- |
| INT          | 整型           | 4字节整数类型，范围约+/-21亿                                 |
| BIGINT       | 长整型         | 8字节整数类型，范围约+/-922亿亿                              |
| REAL         | 浮点型         | 4字节浮点数，范围约+/-1038                                   |
| DOUBLE       | 浮点型         | 8字节浮点数，范围约+/-10308                                  |
| DECIMAL(M,N) | 高精度小数     | 由用户指定精度的小数，例如，DECIMAL(20,10)表示一共20位，其中小数10位，通常用于财务计算 |
| CHAR(N)      | 定长字符串     | 存储指定长度的字符串，例如，CHAR(100)总是存储100个字符的字符串 |
| VARCHAR(N)   | 变长字符串     | 存储可变长度的字符串，例如，VARCHAR(100)可以存储0~100个字符的字符串 |
| BOOLEAN      | 布尔类型       | 存储True或者False                                            |
| DATE         | 日期类型       | 存储日期，例如，2018-06-22                                   |
| TIME         | 时间类型       | 存储时间，例如，12:20:59                                     |
| DATETIME     | 日期和时间类型 | 存储日期+时间，例如，2018-06-22 12:20:59                     |

# 主键

选取主键的一个基本原则是：不使用任何业务相关的字段作为主键。

因此，身份证号、手机号、邮箱地址这些看上去可以唯一的字段，均*不可*用作主键。

作为主键最好是完全业务无关的字段，我们一般把这个字段命名为`id`。常见的可作为`id`字段的类型有：

1. 自增整数类型：数据库会在插入数据时自动为每一条记录分配一个自增整数，这样我们就完全不用担心主键重复，也不用自己预先生成主键；
2. 全局唯一GUID类型：使用一种全局唯一的字符串作为主键，类似`8f55d96b-8acc-4636-8cb8-76bf8abc2f57`。GUID算法通过网卡MAC地址、时间戳和随机数保证任意计算机在任意时间生成的字符串都是不同的，大部分编程语言都内置了GUID算法，可以自己预算出主键。

对于大部分应用来说，通常自增类型的主键就能满足需求。我们在`students`表中定义的主键也是`BIGINT NOT NULL AUTO_INCREMENT`类型

* 联合主键

### 联合主键

关系数据库实际上还允许通过多个字段唯一标识记录，即两个或更多的字段都设置为主键，这种主键被称为联合主键。

对于联合主键，允许一列有重复，只要不是所有主键列都重复即可

# 索引

To make changes to an existing table called "students," you can use the SQL command `ALTER TABLE`. 

1. Adding a new column:

```mysql
ALTER TABLE students
ADD COLUMN age INT;
```

2. Renaming a column:

```
sqlCopy codeALTER TABLE students
RENAME COLUMN age TO student_age;
```

This renames the "age" column in the "students" table to "student_age".

3. Dropping a column:

```
sqlCopy codeALTER TABLE students
DROP COLUMN student_age;
```



如果要经常根据`score`列进行查询，就可以对`score`列创建索引：

```mysql
ALTER TABLE students
ADD INDEX idx_score (score);
```

使用`ADD INDEX idx_score (score)`就创建了一个名称为`idx_score`，使用列`score`的索引。索引名称是任意的，索引如果有多列，可以在括号里依次写上

```mysql
ALTER TABLE students
ADD INDEX idx_name_score (name, score);
```



但是，这些列根据业务要求，又具有唯一性约束：即不能出现两条记录存储了同一个身份证号。这个时候，就可以给该列添加一个唯一索引。例如，我们假设`students`表的`name`不能重复：

```
ALTER TABLE students
ADD UNIQUE INDEX uni_name (name);
```

通过`UNIQUE`关键字我们就添加了一个唯一索引。

# 查询操作

要查询数据库表的数据，我们使用如下的SQL语句：

```
SELECT * FROM <表名>
```

假设表名是`students`，要查询`students`表的所有行，我们用如下SQL语句：

```mysql
SELECT 100+200
```

使用SELECT查询的基本语句`SELECT * FROM <表名>`可以查询一个表的所有行和所有列的数据。

SELECT查询的结果是一个二维表。

* 筛选查询

```mysql
SELECT * FROM <表名> WHERE <条件表达式>
```

* 用多个条件筛选

> 条件表达式可以用`<条件1> AND <条件2>`表达满足条件1并且满足条件2。例如，符合条件“分数在80分或以上”，并且还符合条件“男生”

```mysql
SELECT * FROM students WHERE score >= 80 AND gender = 'M';
```

* 或者

> 第二种条件是`<条件1> OR <条件2>`，表示满足条件1或者满足条件2。例如，把上述`AND`查询的两个条件改为`OR`，查询结果就是“分数在80分或以上”或者“男生”

```mysql
SELECT * FROM students WHERE score >= 80 OR gender = 'M';
```

* 非条件

> 第三种条件是`NOT <条件>`，表示“不符合该条件”的记录。例如，写一个“不是2班的学生”这个条件，可以先写出“是2班的学生”：`class_id = 2`，再加上`NOT`：`NOT class_id = 2`

```my
SELECT * FROM students WHERE NOT class_id = 2;
```

# 投影查询

> 使用`SELECT * FROM <表名> WHERE <条件>`可以选出表中的若干条记录。我们注意到返回的二维表结构和原表是相同的，即结果集的所有列与原表的所有列都一一对应。
>
> 如果我们只希望返回某些列的数据，而不是所有列的数据，我们可以用`SELECT 列1, 列2, 列3 FROM ...`，让结果集仅包含指定列。这种操作称为投影查询。



> 从`students`表中返回`id`、`score`和`name`这三列
>
> ```mysql
> SELECT id, score, name FROM students;
> ```

* 结果集的列的顺序和原表可以不一样。



> 使用`SELECT 列1, 列2, 列3 FROM ...`时，还可以给每一列起个别名，这样，结果集的列名就可以与原表的列名不同。它的语法是`SELECT 列1 别名1, 列2 别名2, 列3 别名3 FROM ...`。
>
> 例如，以下`SELECT`语句将列名`score`重命名为`points`，而`id`和`name`列名保持不变：

```mysql
SELECT id, score points, name FROM students;
```



# 排序

* 默认的排序规则是`ASC`：“升序”，即从小到大。`ASC`可以省略，即`ORDER BY score ASC`和`ORDER BY score`效果一样。



> 可以实现在查询的时候使用`ORDER BY`子句来排序

```mysql
SELECT id, name, gender, score FROM students ORDER BY score;
SELECT id, name, gender, score FROM students ORDER BY score DESC;
```



> 可以使用多个关键字来进行排序然后输出

```mysql
SELECT id, name, gender, score FROM students ORDER BY score DESC, gender;
```

* 使用`ORDER BY score DESC, gender`表示先按`score`列倒序，如果有相同分数的，再按`gender`列排序



# 分页查询

> 分页实际上就是从结果集中“截取”出第M~N条记录。这个查询可以通过`LIMIT <N-M> OFFSET <M>`子句实现。我们先把所有学生按照成绩从高到低进行排序

```mysql
SELECT id, name, gender, score FROM students ORDER BY score DESC;

SELECT id, name, gender, score
FROM students
ORDER BY score DESC
LIMIT 3 OFFSET 0;
```

* 上述查询`LIMIT 3 OFFSET 0`表示，对结果集从0号记录开始，最多取3条。注意SQL记录集的索引从0开始。

* 如果要查询第2页，那么我们只需要“跳过”头3条记录，也就是对结果集从3号记录开始查询，把`OFFSET`设定为3

* 使用下标进行索引



> 查询第4页的时候，`OFFSET`应该设定为9:

```mysql
SELECT id, name, gender, score
FROM students
ORDER BY score DESC
LIMIT 3 OFFSET 9;
```

* 由于第4页只有1条记录，因此最终结果集按实际数量1显示。`LIMIT 3`表示的意思是“最多3条记录”。



- `LIMIT`总是设定为`pageSize`；
- `OFFSET`计算公式为`pageSize * (pageIndex - 1)`。



> 当我们筛选的时候,筛选的结果是空的时候,或者,在分页查找的时候查找到了空的结果.
>
> 返回
>
> ```mysql
> Empty result set
> ```



# 聚合查询

> 仍然以查询`students`表一共有多少条记录为例，我们可以使用SQL内置的`COUNT()`函数查询
>
> * 查询的时候是多少个记录(行数)

> 使用聚合查询时，我们应该给列名设置一个别名，便于处理结果：
>
> ```mysql
> SELECT COUNT(*) num FROM students;
> ```



* 同时可以使用`WHERE`来筛选

```mysql
SELECT COUNT(*) boys FROM students WHERE gender = 'M';
```



| 函数 | 说明                                   |
| :--- | :------------------------------------- |
| SUM  | 计算某一列的合计值，该列必须为数值类型 |
| AVG  | 计算某一列的平均值，该列必须为数值类型 |
| MAX  | 计算某一列的最大值                     |
| MIN  | 计算某一列的最小值                     |



* 要特别注意：如果聚合查询的`WHERE`条件没有匹配到任何行，`COUNT()`会返回0，而`SUM()`、`AVG()`、`MAX()`和`MIN()`会返回`NULL`



> ```mysql
> SELECT * FROM students, classes;
> ```
>
> 这种一次查询两个表的数据，查询的结果也是一个二维表，它是`students`表和`classes`表的“乘积”，即`students`表的每一行与`classes`表的每一行都两两拼在一起返回。结果集的列数是`students`表和`classes`表的列数之和，行数是`students`表和`classes`表的行数之积。



> 这种多表查询又称笛卡尔查询，使用笛卡尔查询时要非常小心，由于结果集是目标表的行数乘积，对两个各自有100行记录的表进行笛卡尔查询将返回1万条记录，对两个各自有1万行记录的表进行笛卡尔查询将返回1亿条记录。



# 多表查询

```mysql
SELECT
    students.id sid,
    students.name,
    students.gender,
    students.score,
    classes.id cid,
    classes.name cname
FROM students, classes;
```



# 链接查询

> 但是，假设我们希望结果集同时包含所在班级的名称，上面的结果集只有`class_id`列，缺少对应班级的`name`列。
>
> 现在问题来了，存放班级名称的`name`列存储在`classes`表中，只有根据`students`表的`class_id`，找到`classes`表对应的行，再取出`name`列，就可以获得班级名称。
>
> 这时，连接查询就派上了用场。我们先使用最常用的一种内连接——INNER JOIN来实现.

```mysql
SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score
FROM students s
INNER JOIN classes c
ON s.class_id = c.id;
```



> 1. 先确定主表，仍然使用`FROM <表1>`的语法；
> 2. 再确定需要连接的表，使用`INNER JOIN <表2>`的语法；
> 3. 然后确定连接条件，使用`ON <条件...>`，这里的条件是`s.class_id = c.id`，表示`students`表的`class_id`列与`classes`表的`id`列相同的行需要连接；
> 4. 可选：加上`WHERE`子句、`ORDER BY`等子句。



* 有内连接（INNER JOIN）就有外连接（OUTER JOIN）

```mysql
SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score
FROM students s
RIGHT OUTER JOIN classes c
ON s.class_id = c.id
ORDER BY score;
```



> INNER JOIN只返回同时存在于两张表的行数据，由于`students`表的`class_id`包含1，2，3，`classes`表的`id`包含1，2，3，4，所以，INNER JOIN根据条件`s.class_id = c.id`返回的结果集仅包含1，2，3。
>
> RIGHT OUTER JOIN返回右表都存在的行。如果某一行仅在右表存在，那么结果集就会以`NULL`填充剩下的字段。
>
> LEFT OUTER JOIN则返回左表都存在的行。如果我们给students表增加一行，并添加class_id=5，由于classes表并不存在id=5的行，所以，LEFT OUTER JOIN的结果会增加一行，对应的`class_name`是`NULL`
>
> 使用FULL OUTER JOIN，它会把两张表的所有记录全部选择出来，并且，自动把对方不存在的列填充为NULL



# 修改信息

## 插入操作

> 当我们需要向数据库表中插入一条新记录时，就必须使用`INSERT`语句
>
> `INSERT`语句的基本语法是：
>
> ```mysql
> INSERT INTO students (class_id, name, gender, score) VALUES (2, '大牛', 'M', 80);
> -- 查询并观察结果:
> SELECT * FROM students;
> ```
>
> 
>
> ```mysql
> INSERT INTO <表名> (字段1, 字段2, ...) VALUES (值1, 值2, ...);
> ```



> 注意到我们并没有列出`id`字段，也没有列出`id`字段对应的值，这是因为`id`字段是一个自增主键，它的值可以由数据库自己推算出来。此外，如果一个字段有默认值，那么在`INSERT`语句中也可以不出现。
>
> 要注意，字段顺序不必和数据库表的字段顺序一致，但值的顺序必须和字段顺序一致。也就是说，可以写`INSERT INTO students (score, gender, name, class_id) ...`，但是对应的`VALUES`就得变成`(80, 'M', '大牛', 2)`。



## 更新信息

> `UPDATE`语句的基本语法是：
>
> ```mysql
> UPDATE <表名> SET 字段1=值1, 字段2=值2, ... WHERE ...;
> ```



> 在`UPDATE`语句中，更新字段时可以使用表达式。例如，把所有80分以下的同学的成绩加10分
>
> ```mysql
> UPDATE students SET score=score+10 WHERE score<80;
> -- 查询并观察结果:
> SELECT * FROM students;
> ```



* 如果`WHERE`条件没有匹配到任何记录，`UPDATE`语句不会报错，也不会有任何记录被更新。



> 最后，要特别小心的是，`UPDATE`语句可以没有`WHERE`条件，例如：
>
> ```
> UPDATE students SET score=60;
> ```
>
> 这时，整个表的所有记录都会被更新。所以，在执行`UPDATE`语句时要非常小心，最好先用`SELECT`语句来测试`WHERE`条件是否筛选出了期望的记录集，然后再用`UPDATE`更新。



## 删除信息

`DELETE`语句的基本语法是：

```mysql
DELETE FROM <表名> WHERE ...;
```

```mysql
DELETE FROM students WHERE id>=5 AND id<=7;
-- 查询并观察结果:
SELECT * FROM students;
```



> 如果`WHERE`条件没有匹配到任何记录，`DELETE`语句不会报错，也不会有任何记录被删除。



> 最后，要特别小心的是，和`UPDATE`类似，不带`WHERE`条件的`DELETE`语句会删除整个表的数据：
>
> ```
> DELETE FROM students;
> ```
>
> 这时，整个表的所有记录都会被删除。所以，在执行`DELETE`语句时也要非常小心，最好先用`SELECT`语句来测试`WHERE`条件是否筛选出了期望的记录集，然后再用`DELETE`删除。



# 管理SQL

在一个运行MySQL的服务器上，实际上可以创建多个数据库（Database）。要列出所有数据库，使用命令：

```mysql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| shici              |
| sys                |
| test               |
| school             |
+--------------------+
```



* 注意：在MySQL命令行客户端输入SQL后，记得加一个`;`表示SQL语句结束，再回车就可以执行该SQL语句。虽然有些SQL命令不需要`;`也能执行，但类似`SELECT`等语句不加`;`会让MySQL客户端换行后继续等待输入。如果在图形界面或程序开发中集成SQL则不需要加`;`。



* 创建数据库

要创建一个新数据库，使用命令：

```mysql
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.01 sec)
```

* 删除数据库

要删除一个数据库，使用命令：

```mysql
mysql> DROP DATABASE test;
Query OK, 0 rows affected (0.01 sec)
```

* 对这个数据库处理

对一个数据库进行操作时，要首先将其切换为当前数据库：

```mysql
mysql> USE test;
Database changed
```



# 表

列出当前数据库的所有表，使用命令：

```mysql
mysql> SHOW TABLES;
+---------------------+
| Tables_in_test      |
+---------------------+
| classes             |
| statistics          |
| students            |
| students_of_class1  |
+---------------------+
```

要查看一个表的结构，使用命令：

```mysql
mysql> DESC students;
+----------+--------------+------+-----+---------+----------------+
| Field    | Type         | Null | Key | Default | Extra          |
+----------+--------------+------+-----+---------+----------------+
| id       | bigint(20)   | NO   | PRI | NULL    | auto_increment |
| class_id | bigint(20)   | NO   |     | NULL    |                |
| name     | varchar(100) | NO   |     | NULL    |                |
| gender   | varchar(1)   | NO   |     | NULL    |                |
| score    | int(11)      | NO   |     | NULL    |                |
+----------+--------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```

还可以使用以下命令查看创建表的SQL语句：

```mysql
mysql> SHOW CREATE TABLE students;
+----------+-------------------------------------------------------+
| students | CREATE TABLE `students` (                             |
|          |   `id` bigint(20) NOT NULL AUTO_INCREMENT,            |
|          |   `class_id` bigint(20) NOT NULL,                     |
|          |   `name` varchar(100) NOT NULL,                       |
|          |   `gender` varchar(1) NOT NULL,                       |
|          |   `score` int(11) NOT NULL,                           |
|          |   PRIMARY KEY (`id`)                                  |
|          | ) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8 |
+----------+-------------------------------------------------------+
1 row in set (0.00 sec)
```

创建表使用`CREATE TABLE`语句，而删除表使用`DROP TABLE`语句：

```mysql
mysql> DROP TABLE students;
Query OK, 0 rows affected (0.01 sec)
```

## 对表的操作

修改表就比较复杂。如果要给`students`表新增一列`birth`，使用：

```mysql
ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL;
```

> 在SQL中，"NOT NULL"是一个约束（constraint），用于指定某个列（column）不允许包含NULL值。NULL表示缺少值或未知值，而"NOT NULL"约束要求该列的每个行都必须包含一个非NULL值。
>
> 当在列上应用"NOT NULL"约束时，它会强制要求在插入或更新数据时必须提供该列的值。如果尝试在没有提供值的情况下插入或更新行，数据库系统将返回错误并拒绝操作。
>
> 在上述例子中，`ALTER TABLE students ADD COLUMN birth VARCHAR(10) NOT NULL;`语句中的"NOT NULL"约束要求在"students"表的"birth"列中，每个行都必须包含一个非NULL的值。这意味着在插入或更新数据时，必须为"birth"列提供一个非NULL的值，否则会引发错误。

要修改`birth`列，例如把列名改为`birthday`，类型改为`VARCHAR(20)`：

```mysql
ALTER TABLE students CHANGE COLUMN birth birthday VARCHAR(20) NOT NULL;
```

* 替换

如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就先删除原记录，再插入新记录。此时，可以使用`REPLACE`语句，这样就不必先查询，再决定是否先删除再插入：

```
REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```

若`id=1`的记录不存在，`REPLACE`语句将插入新记录，否则，当前`id=1`的记录将被删除，然后再插入新记录。

* 插入更新

如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就更新该记录，此时，可以使用`INSERT INTO ... ON DUPLICATE KEY UPDATE ...`语句：

```mysql
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;
```

若`id=1`的记录不存在，`INSERT`语句将插入新记录，否则，当前`id=1`的记录将被更新，更新的字段由`UPDATE`指定。

> The ON DUPLICATE KEY clause is used in an INSERT statement to handle situations where a new row being inserted would violate a uniqueness constraint, such as a primary key or a unique index.
>
> When an INSERT statement encounters a duplicate key violation, instead of throwing an error and aborting the operation, the ON DUPLICATE KEY clause allows you to specify an alternative action to be taken. This clause gives you the ability to update existing rows with new values or perform any other desired action.
>
> The syntax for the ON DUPLICATE KEY clause is as follows:
>
> ```sql
> ON DUPLICATE KEY UPDATE column1 = value1, column2 = value2, ...
> ```
>
> Here, "column1 = value1, column2 = value2, ..." represents the columns and their corresponding values that you want to update if a duplicate key violation occurs.
>
> By using the ON DUPLICATE KEY UPDATE clause, you can handle duplicate key violations gracefully and control the behavior of the INSERT statement accordingly. Instead of failing the entire operation, it allows you to choose whether to update the existing row or perform other actions based on your specific requirements.

* 纯插入操作

> 插入或忽略

如果我们希望插入一条新记录（INSERT），但如果记录已经存在，就啥事也不干直接忽略，此时，可以使用`INSERT IGNORE INTO ...`语句：

```
INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);
```

若`id=1`的记录不存在，`INSERT`语句将插入新记录，否则，不执行任何操作。

## 快照

如果想要对一个表进行快照，即复制一份当前表的数据到一个新表，可以结合`CREATE TABLE`和`SELECT`：

```
-- 对class_id=1的记录进行快照，并存储为新表students_of_class1:
CREATE TABLE students_of_class1 SELECT * FROM students WHERE class_id=1;
```

新创建的表结构和`SELECT`使用的表结构完全一致。



The SQL statement you provided creates a new table named "statistics" with the specified columns and constraints. Here's the breakdown of the CREATE TABLE statement:

```sql
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
```

This statement creates a table named "statistics" with the following columns:

1. "id": BIGINT data type, which is a large integer.
   - NOT NULL: Specifies that the "id" column cannot contain NULL values.
   - AUTO_INCREMENT: Indicates that the values for this column will be automatically generated and incremented for each new row inserted.

2. "class_id": BIGINT data type, which is a large integer.
   - NOT NULL: Specifies that the "class_id" column cannot contain NULL values.

3. "average": DOUBLE data type, which is a double-precision floating-point number.
   - NOT NULL: Specifies that the "average" column cannot contain NULL values.

The PRIMARY KEY constraint is applied to the "id" column, which means it uniquely identifies each row in the table. This constraint ensures that the "id" column will have unique values, and it also automatically creates an index on this column.

Overall, this CREATE TABLE statement defines the structure of the "statistics" table with the specified columns and constraints.



## 写入查询结果集

如果查询结果集需要写入到表中，可以结合`INSERT`和`SELECT`，将`SELECT`语句的结果集直接插入到指定表中。

例如，创建一个统计成绩的表`statistics`，记录各班的平均成绩：

```
CREATE TABLE statistics (
    id BIGINT NOT NULL AUTO_INCREMENT,
    class_id BIGINT NOT NULL,
    average DOUBLE NOT NULL,
    PRIMARY KEY (id)
);
```

然后，我们就可以用一条语句写入各班的平均成绩：

```
INSERT INTO statistics (class_id, average) SELECT class_id, AVG(score) FROM students GROUP BY class_id;
```

确保`INSERT`语句的列和`SELECT`语句的列能一一对应，就可以在`statistics`表中直接保存查询的结果：

```mysql
> SELECT * FROM statistics;
+----+----------+--------------+
| id | class_id | average      |
+----+----------+--------------+
|  1 |        1 |         86.5 |
|  2 |        2 | 73.666666666 |
|  3 |        3 | 88.333333333 |
+----+----------+--------------+
3 rows in set (0.00 sec)
```



在查询的时候，数据库系统会自动分析查询语句，并选择一个最合适的索引。但是很多时候，数据库系统的查询优化器并不一定总是能使用最优索引。如果我们知道如何选择索引，可以使用`FORCE INDEX`强制查询使用指定的索引。例如：

```
> SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;
```

指定索引的前提是索引`idx_class_id`必须存在



# 事务

> 可见，数据库事务具有ACID这4个特性：
>
> - A：Atomic，原子性，将所有SQL作为原子工作单元执行，要么全部执行，要么全部不执行；
> - C：Consistent，一致性，事务完成后，所有数据的状态都是一致的，即A账户只要减去了100，B账户则必定加上了100；
> - I：Isolation，隔离性，如果有多个事务并发执行，每个事务作出的修改必须与其他事务隔离；
> - D：Duration，持久性，即事务完成后，对数据库数据的修改被持久化存储。



* 对于单条SQL语句，数据库系统自动将其作为一个事务执行，这种事务被称为*隐式事务*。

* 要手动把多条SQL语句作为一个事务执行，使用`BEGIN`开启一个事务，使用`COMMIT`提交一个事务，这种事务被称为*显式事务*，例如，把上述的转账操作作为一个显式事务：

  ```mysql
  BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  COMMIT;
  ```

* 有些时候，我们希望主动让事务失败，这时，可以用`ROLLBACK`回滚事务，整个事务会失败：

  ```mysql
  BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
  ROLLBACK;
  ```



SQL标准定义了4种隔离级别，分别对应可能出现的数据不一致的情况：

| Isolation Level  | 脏读（Dirty Read） | 不可重复读（Non Repeatable Read） | 幻读（Phantom Read） |
| :--------------- | :----------------- | :-------------------------------- | :------------------- |
| Read Uncommitted | Yes                | Yes                               | Yes                  |
| Read Committed   | -                  | Yes                               | Yes                  |
| Repeatable Read  | -                  | -                                 | Yes                  |
| Serializable     | -                  | -                                 | -                    |



## READ UNCOMMITED

Read Uncommitted是隔离级别最低的一种事务级别。在这种隔离级别下，一个事务会读到另一个事务更新后但未提交的数据，如果另一个事务回滚，那么当前事务读到的数据就是脏数据，这就是脏读（Dirty Read）。



## READ COMMITED

在Read Committed隔离级别下，一个事务可能会遇到不可重复读（Non Repeatable Read）的问题。

不可重复读是指，在一个事务内，多次读同一数据，在这个事务还没有结束时，如果另一个事务恰好修改了这个数据，那么，在第一个事务中，两次读取的数据就可能不一致。



## REPEATABLE READ

在Repeatable Read隔离级别下，一个事务可能会遇到幻读（Phantom Read）的问题。

幻读是指，在一个事务中，第一次查询某条记录，发现没有，但是，当试图更新这条不存在的记录时，竟然能成功，并且，再次读取同一条记录，它就神奇地出现了。



