constraints 约束

redundancy 冗余

inconsistancy 不一致

transction 事务

normalization 规范化



现在我们需要DBMS(数据库管理系统)帮助我们管理数据库

使用SQL语言来修改数据库



transaction



E/R model 从现实世界中抽象出来的信息模型,其中是我们需要保存的数据



## 层级

1. external level = user level
2. conceptual level = logical level
3. internal level = physical level 

# 绪论

`定义`a database is a collection of persistent information for rapid search and retrieval 

inforation 自然化的

data 在表格化的结构化的地方的数据



DBMS可以自动处理脏读的问题,使得问题一个一个执行.



## why database

1. 数据可以分享
2. 处理数据重复的问题(redundancy)
3. 不一致可以被避免(inconsistence)
4. 参照完整性,修改一个表单中的内容的时候,同时会修改相关引用的数据(intergrity can be maintained)
5. 访问数据十分方便.(data accessing can be conventient)
6. transaction can be provided,当一连串的事件不能之前执行的时候使用回滚(roll back)



## 特点

massive 

persistent 

safe/reliable

mutli-user

convenient

efficient



# DB LANGUAGE



## DDL(database define language)

`CREATE DATABASE <databaseName>`

`USE <databse name>`

`DROP DATABASE <database name>` 

`CREATE TABLE <table name>(list of elements)`

> 元素的列表的构成(元素之间使用`,`分割)
>
> `属性的名字,属性的类型`->basic element

> 属性的类型
>
> 1. INT/INTEGER
> 2. REAL/FLOAT
> 3. CHAR(n) 固定个数的字符
> 4. VARCHAR(n) 至多多少个数的字符数组
> 5. TIME 需要提供它的样式
> 6. DATE 需要提供它的样式



## DML(database manipulation language)



## DCL(databse control language)



# DATA MODEL

relation = table



constraints : 键

key constraints : 关键键



## 类型

graph data model 

> 有节点和边构成的图

> 难以删除和插入
>
> 数据大的时候难以使用
>
> 管理语言困难

hierarchical data model

> 有层次的数据
>
> 很像树结构

> 处理数据的时候需要从上到下
>
> 删除数据的时候会造成别的数据丢失

realtional data model

> 如同列表一样的存储方式



# 关系型数据模型

key constraints : 不可重复的内容

foreign key : 外键,和别的表一起使用的数据

外键（Foreign Key）是关系数据库中的一个重要概念，用于建立表与表之间的关联关系。外键定义了一个表中的一个或多个列，这些列的值必须与另一个表中的主键或唯一键列的值匹配。外键用于确保数据的完整性和一致性，以维护表之间的关联性。

以下是有关外键的一些关键点：

1. **外键与主键关联**：外键的值与另一个表的主键或唯一键关联。这种关联创建了表与表之间的引用关系，通常表示为从一个表（子表）指向另一个表（主表）的关系。

2. **确保数据完整性**：外键确保了在关联表之间维护一致性和数据完整性。它防止了插入或更新行，使它们引用不存在的值。

3. **CASCADE 操作**：外键可以定义级联操作，以确定当主表的记录更改或删除时子表中的相关记录的行为。例如，CASCADE DELETE 将删除子表中与主表记录相关的行。

4. **防止孤立数据**：外键可以防止在关联表之间创建孤立的、没有关联的数据。这确保了数据的连贯性。

5. **语法示例**：在创建表时，可以使用FOREIGN KEY关键字定义外键。以下是一个SQL示例：

   ```sql
   CREATE TABLE Orders (
       OrderID INT PRIMARY KEY,
       ProductID INT,
       OrderDate DATE,
       FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
   );
   ```

   在此示例中，"Orders"表中的"ProductID"列是外键，它引用了"Products"表的"ProductID"列作为主键。

总之，外键是数据库设计中的重要元素，用于维护表之间的关联性和数据完整性。通过定义外键，您可以确保数据在不同表之间的一致性，并允许执行复杂的数据关系查询。



## attribute(属性名)

`定义`第一行的属性名就是`attribute`,the header of a column in a table(relation)



### key

* 不可重复

可以是多个

> 存在`primary key`



## schemas

`定义`属性名(attributes)的集合,一般我们使用标准顺序表示,也就是它本质是一个集合

* 直接使用`attribute list`表示好了

比如`student(ID,name,GPA)`.



## tuple

`定义`a tuple is a row beside the header row in a relation.一行的数据叫做一个tuple

> 用来表示数据的条数
>
> 本质是有序的列表



## domains(域)

在关系数据库中，"Domain"（域）通常指的是一组允许的数据值。它定义了特定列（字段）中可以包含的值的类型和范围。域是数据库中数据类型的抽象，它可以应用于一个或多个表中的列，以确保数据的一致性和完整性。以下是关于域的一些关键点：

1. **数据类型定义**：域定义了列中数据的类型，例如整数、字符、日期、布尔值等。这有助于确保列中的数据与其定义的域类型一致。

2. **范围和约束**：域可以定义特定列中允许的值的范围和约束条件。这包括最小值、最大值、默认值、唯一性、非空性等。这有助于确保数据的完整性，防止不合法的数据进入数据库。

3. **复用性**：域可以在一个或多个表中复用。这意味着如果多个表需要相同类型的数据，您可以定义一个域，然后在这些表的相应列中使用该域。

4. **可读性和维护性**：使用域可以提高数据库的可读性和维护性。它允许您为特定列提供有意义的名称，而不是仅仅指定原始数据类型。

5. **示例**：以下是一个示例，展示了如何在创建表时使用域：

   ```sql
   CREATE DOMAIN Phone AS VARCHAR(15)
   CHECK (VALUE ~ '^\d{3}-\d{3}-\d{4}$');
   
   CREATE TABLE Customers (
       CustomerID INT PRIMARY KEY,
       CustomerName VARCHAR(50),
       PhoneNumber Phone
   );
   ```

   在此示例中，我们定义了一个名为"Phone"的域，它规定了电话号码的格式。然后，在"Customers"表中，我们使用了这个域类型来定义"PhoneNumber"列，以确保电话号码的一致性和格式正确。

总之，域是数据库设计中的有用工具，它有助于确保数据的一致性、完整性和可读性，同时减少了重复定义数据类型的工作。它们对于数据库的结构和数据质量都非常有价值。



## relation instance 

关系实例（Relation Instance）是关系数据库理论中的一个概念，它指的是关系模式（Relation Schema）中实际数据的集合，也就是表中的具体数据行。在关系数据库中，表是用来存储数据的结构，而表中的每一行代表了一个实际的数据记录。

以下是关于关系实例的一些关键点：

1. **数据记录**：关系实例是实际的数据记录集合，它包括了表中的每一行。每一行代表了某个实体或对象的属性值。

2. **表格结构**：关系实例是根据与关系模式（表结构）相对应的表格结构组织的。表结构定义了表的列和每列的数据类型。

3. **实例和模式的关系**：关系实例与关系模式之间存在关联。模式定义了表的结构，包括列名和数据类型，而实例是模式的具体实例化，是实际数据的载体。

4. **示例**：以下是一个示例，展示了关系实例的概念。假设有一个名为"Employees"的关系模式，它包括列"EmployeeID"、"FirstName"、"LastName"等。那么以下是一个"Employees"关系实例的示例：

   | EmployeeID | FirstName | LastName | Salary |
   | ---------- | --------- | -------- | ------ |
   | 101        | John      | Smith    | 50000  |
   | 102        | Alice     | Johnson  | 55000  |
   | 103        | Bob       | Brown    | 60000  |

   在这个示例中，"Employees"关系模式定义了表格的结构，而表格中的数据行（每行代表一个员工）构成了关系实例。

总之，关系实例是关系数据库中存储的实际数据，它们与关系模式一起构成了数据库的基本组成部分。数据库管理系统（DBMS）用于存储、检索和管理关系实例，以提供数据的有效组织和访问。



## equivalent representations of a relation

`定义`是元组的集合,不是列表

* 注意,行的顺序和列的顺序都不重要,所以,比如3个attributes的header,可能的表示方式是`3*2*1`(3!)个.



> 表现的顺序是实时更新的. 



# SQL



## CREATE

使用`CREATE TABLE table_name(...)`创建列表



## ALTER

ALTER 操作是用于修改数据库表的结构（模式）的 SQL 命令。它允许您在已经存在的表中添加、修改或删除列、修改表的约束条件以及执行其他结构性的更改。以下是一些 ALTER 操作的常见用法：

1. **添加列**：您可以使用 ALTER TABLE 命令来向已存在的表中添加新列。例如：

   ```sql
   ALTER TABLE table_name
   ADD column_name datatype;
   ```

   这将在表中添加一个新的列，其中 column_name 是列的名称，datatype 是数据类型。

2. **修改列**：您可以使用 ALTER TABLE 命令修改已存在列的数据类型或约束条件。例如：

   ```sql
   ALTER TABLE table_name
   ALTER COLUMN column_name SET DATA TYPE new_datatype;
   ```

   这将修改列的数据类型。

3. **删除列**：您可以使用 ALTER TABLE 命令删除表中的列。例如：

   ```sql
   ALTER TABLE table_name
   DROP COLUMN column_name;
   ```

   这将删除指定的列及其数据。

4. **添加约束**：您可以使用 ALTER TABLE 命令来添加新的约束条件，如主键、外键或唯一键。例如：

   ```sql
   ALTER TABLE table_name
   ADD CONSTRAINT constraint_name constraint_type (column_name);
   ```

   这将为表添加一个新的约束条件。

5. **删除约束**：您可以使用 ALTER TABLE 命令删除已存在的约束条件。例如：

   ```sql
   ALTER TABLE table_name
   DROP CONSTRAINT constraint_name;
   ```

   这将删除指定的约束条件。

6. **重命名表**：您可以使用 ALTER TABLE 命令重命名已存在的表。例如：

   ```sql
   ALTER TABLE old_table_name
   RENAME TO new_table_name;
   ```

   这将修改表的名称。

请注意，ALTER 操作可能因数据库管理系统的不同而有些许差异，语法也可能会有所不同。在执行 ALTER 操作之前，请确保备份重要数据，并小心谨慎地进行操作，以防止意外数据丢失或表结构损坏。



## 修改操作

1. insert
2. delete
3. update



## insert

`INSERT` 命令是 SQL 中用于将新数据插入到数据库表中的命令。它是数据库操作中的一种基本操作，允许您将新的行（记录）添加到数据库表中。以下是关于 `INSERT` 命令的基本介绍：

语法格式：

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

- `INSERT INTO`：指定要插入数据的目标表。
- `table_name`：要插入数据的表名。
- `(column1, column2, column3, ...)`：指定要插入数据的列（可选，如果不指定列，则需要提供与表中列相同数量和顺序的值）。
- `VALUES`：指定要插入的值。
- `(value1, value2, value3, ...)`：指定要插入的实际数据值，与列的顺序对应。

示例：

假设有一个名为 "Customers" 的表格，包括了 "CustomerID"、"FirstName" 和 "LastName" 列，我们可以使用 `INSERT` 命令来插入新的客户数据：

```sql
INSERT INTO Customers (CustomerID, FirstName, LastName)
VALUES (1, 'John', 'Doe');
```

这个命令将在 "Customers" 表中插入一行新的数据，包括了客户ID、名字和姓氏。

重要注意事项：
- `INSERT` 命令要求提供要插入的表名和对应列的值。
- 列名和值之间必须一一对应，且数据类型必须与表的定义相匹配。
- 如果省略列名，需要提供与表中列相同数量和顺序的值。
- 如果插入的数据违反了表中的约束条件（例如，主键或唯一性约束），则插入操作会失败。
- 在大多数数据库管理系统中，`INSERT` 命令执行成功后会返回插入的行数或生成的主键值（如果有的话）。

`INSERT` 命令是一种常用的数据库操作，用于向数据库中添加新数据，通常与应用程序的数据输入过程密切相关。



* 可以设定列表的内容其中的几个attribute,不需要传递全部的值.
* 如果你省略表的attributes,你需要提供与表中列相同数量和顺序的值



## delete

`DELETE` 命令是 SQL 中用于从数据库表中删除行（记录）的命令。它允许您删除满足特定条件的行，从而使数据库中的数据发生变化。以下是关于 `DELETE` 命令的基本介绍：

语法格式：

```sql
DELETE FROM table_name
WHERE condition;
```

- `DELETE FROM`：指定要从中删除行的目标表。
- `table_name`：要从中删除行的表名。
- `WHERE`：可选，用于指定删除哪些行的条件。
- `condition`：可选，是一个布尔表达式，用于确定哪些行将被删除。如果省略 `WHERE` 子句，将删除表中的所有行。

示例：

假设有一个名为 "Customers" 的表格，包括了 "CustomerID"、"FirstName" 和 "LastName" 列，我们可以使用 `DELETE` 命令来删除满足特定条件的客户数据，例如：

```sql
DELETE FROM Customers
WHERE CustomerID = 1;
```

这个命令将删除 "Customers" 表中 `CustomerID` 为 1 的客户数据。

重要注意事项：
- `DELETE` 命令会永久性地从表中删除行，因此在使用之前请慎重考虑。
- 如果省略 `WHERE` 子句，`DELETE` 命令将删除表中的所有行，这通常不是预期的操作，因此要谨慎使用。
- `WHERE` 子句用于指定删除哪些行。只有满足条件的行才会被删除。
- 在执行 `DELETE` 命令之前，最好先使用 `SELECT` 命令测试 `WHERE` 子句，以确保选择了正确的行。
- 删除操作通常需要足够的权限，因此请确保具有足够的权限来执行删除操作。

`DELETE` 命令是管理数据库数据的重要工具，它允许您删除不再需要的数据或根据特定条件执行数据清理操作。



## update

用来批量更新表内的数据

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

- `UPDATE`：指定要更新数据的目标表。
- `table_name`：要更新数据的表名。
- `SET`：指定要修改的列以及它们的新值。
- `column1 = value1, column2 = value2, ...`：列名和新值的对应关系。您可以一次更新多列。
- `WHERE`：可选，用于指定哪些行将被更新的条件。
- `condition`：可选，是一个布尔表达式，用于确定哪些行将被更新。如果省略 `WHERE` 子句，将更新表中的所有行





# 第一次实验

规定至多30字符的字符串

```sql
CREATE TABLE YourTable (
    YourColumn VARCHAR(30) -- 在这里指定最大长度为 30 字符
);
```



* 字符串需要使用单引号`'`



拼接字符串

> 使用`CONCAT`实现

```sql
UPDATE your_table
SET your_column = CONCAT(your_column, '给定的字符串')
WHERE condition;
```



* 删除表的时候使用`DROP`
* 删除数据的时候使用`DELETE`



# relational algebra (使用关系代数)

## operator

1. **关系（Relation）**：在关系代数中，关系是一个包含元组（行）的表，每个元组由属性（列）组成。关系可以表示为 R(A, B, C)，其中 R 是关系的名称，A、B、C 是属性。
2. **选择操作（Selection）**：选择操作用于从关系中选择满足特定条件的元组。它类似于 SQL 中的 WHERE 子句。例如，σ_A>5(R) 表示从关系 R 中选择所有 A 大于 5 的元组。
3. **投影操作（Projection）**：投影操作用于从关系中选择特定属性，以创建一个包含较少属性的新关系。它类似于 SQL 中的 SELECT 子句。例如，π_A, B(R) 表示从关系 R 中选择属性 A 和属性 B，忽略其他属性。
4. **并运算（Union）**：并运算用于将两个关系的元组合并为一个新的关系。它要求两个关系具有相同的属性。例如，R ∪ S 表示关系 R 和关系 S 的并运算。
5. **差运算（Difference）**：差运算用于从一个关系中移除另一个关系中的元组。它也要求两个关系具有相同的属性。例如，R - S 表示从关系 R 中移除与关系 S 中匹配的元组。
6. **交运算（Intersection）**：交运算用于找到两个关系中共同存在的元组。也需要两个关系具有相同的属性。例如，R ∩ S 表示关系 R 和关系 S 的交运算。
7. **笛卡尔积（Cartesian Product）**：笛卡尔积操作用于生成两个关系的所有可能组合的元组。例如，R × S 表示关系 R 和关系 S 的笛卡尔积。
8. **连接运算（Join）**：连接操作用于将两个关系中的元组基于特定条件合并在一起。连接可以是等值连接或非等值连接，用于从多个表中获取相关信息。



从一个表中拿东西
$$
π_{title,year}(movies)
$$

> 下标的内容是需要提取的数据
>
> 括号里面是表的名字

* eliminate duplicate tuples , if any 会自动去重
* 在实际的SQL查询中,不会自动去重


$$
π_{title,year+1}(movies)
$$

> 可以使用表达式来计算列的内容

$$
π_{title,title}(movies)
$$

> 可以构建原本相同的内容的列,但是,这两个列的名字不能一样.


$$
σ_{studioName='Disney'}(movies)
$$

> 筛选条件设置,筛选表中符合条件的全部元素.

* 可以设置`^`作为`and`符号


$$
π_{title,year}(σ_{studioName='Disney'}(movies))
$$

> 可以复合使用


$$
A×B
$$

> 笛卡尔积合并两个集合

* 如果合并的两个表的列的名字是相同的,合并的时候,会使用`A.columnName`和`B.columnName`方式

$$
\sigma_{studioName=name}(A×B)
$$







自然连接（natural join）和θ连接（theta join）都是关系代数中的连接操作，用于将两个关系表中的元组进行匹配。自然连接是在两个表中所有同名属性上进行匹配，而θ连接则是在指定的属性上进行匹配。

自然连接的符号为⋈，θ连接的符号为⋈θ。


$$
⋈_{\theta}\\
\pi_{address}(movies⋈_{studioNmae=name}studio)
$$

> 简化了叉乘然后搜索的部分


$$
A⋈B
$$

> 会去掉重复的一致的属性列,并且只保留有这些一致属性的数据叉乘之后出来的结果

* 相当于自动配对这些相同的部分数据然后组合合并起来


$$
\rho_{s(A1,A2....An)}()
$$

> 使用重命名方式

$$
\rho_{name,title,year}(tableName)
$$


$$
\cap~交集
\\
\cup~并集
$$

> 合并两个数据表


$$
R-S
$$

> 在数据表R中但是不在数据表S中的数据


$$
A\cap B~=~A-(A-B)
$$







$$
A~\div~B
$$

> 满足B数据中所有的内容,并且在A数据中



# 简单的查询使用SQL

clause : 条款

* SQL区分大小写，所以我们需要严格写出



not运算符

```sql
SELECT * FROM table_name WHERE not(....)
```



`*`运算符代表全部的属性

如何在关系代数中不使用`pi`,那么就是查找全部的属性内容,使用`*`运算符.



* `WHERE`不是必要的,不存在`WHERE`的时候,**全正确/都需要返回**



* 保留两位小数

```sql
SELECT cast(minutes as decimal(10,2))...
```



* 往里面添加一个常量

```sql
SELECT year , 'this is a string' as myString ...
```

列的名字是`myString`,这个是修改列名字的写法,并且添加了一个常数属性

> 我们可以使用`as <new name>`的方式来重命名任意一个列的名字



# 状态运算语句的三种可能的结果

1. true
2. false
3. unkown

> 可以认为
>
> true : 1
>
> unkown : 0.5
>
> false :  0
>
> and = min
>
> or = max



# NULL

1. 不可访问,是missing value
2. 不可使用的.



> 状况语句包含三种结果,true/false/unkown
>
> 只有true的时候,成功

* 所有和NULL的比较的值是`UNKOWN`,所以,不能执行



## 找到NULL的值

因为不可以对NULL值使用`=`运算符比较

我们使用`WHERE XXX IS NULL`来比较,这个只返回`true/false`

```sql
WHERE XXX IS NULL
WHERE XXX IS NOT NULL
```



# PATTERN(字符串模式比较)

> 使用`LIKE`运算符

```sql
WHERE RTRIM(title) LIKE 'Star ____'
```



`LIKE` 是 SQL 中用于在字符串比较中进行模糊匹配的操作符。它通常与 `SELECT` 语句的 `WHERE` 子句一起使用，以查找包含特定模式的文本值。`LIKE` 操作符非常有用，尤其当您需要从表中检索符合特定模式的数据时。

`LIKE` 操作符使用两个通配符来匹配文本模式：

1. `%`（百分号）：用于匹配任何字符序列，包括零个字符、一个字符、多个字符等。例如，`'A%'` 匹配以字母 'A' 开头的任何字符串。
2. `_`（下划线）：用于匹配单个字符。例如，`'J_hn'` 匹配以 'J' 开头，然后是任何字符，接着是 'h'，最后是 'n' 的字符串。

以下是 `LIKE` 操作符的基本语法：

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```

- `SELECT column1, column2, ...`：要检索的列列表。
- `FROM table_name`：要检索数据的表。
- `WHERE columnN LIKE pattern`：`LIKE` 操作符的条件，其中 `columnN` 是要比较的列，而 `pattern` 是要匹配的文本模式。

示例：

假设我们有一个名为 "Employees" 的表格，包括了员工的姓名（Name）列。如果我们希望找到所有以 'John' 开头的员工姓名，可以使用 `LIKE` 操作符：

```sql
SELECT Name
FROM Employees
WHERE Name LIKE 'John%';
```

上述查询将返回所有以 'John' 开头的员工姓名。

`LIKE` 操作符在许多情况下非常有用，例如搜索具有特定前缀或后缀的文本，查找包含特定字符序列的数据，或执行其他模糊匹配操作。要根据您的需求构建有效的模式，您可以使用 `%` 和 `_` 通配符。



# 在`''`中使用`'`符号

使用`\'`或者`''`实现一个`'`符号.



# 比较运算符

* 可以用于比较字符串,使用的是字典序比较字符串的方式



## `between`运算符

```sql
WHERE length BETWEEN 116 and 120
等同于
WHERE length >= 116 and length <= 120
```



# `extract`提取运算符

```sql
WHERE extract(year from birthdate) .....
```

可以从一个日期类型中提取一个数字类型的year出来



# `distinct`

去重

```sql
select distinct movieyear from movies
```



# 数据库

physical 物理存储层

comceptual

logical 逻辑层



# view

在 SQL 数据库中，**视图（View）** 是一种虚拟表，它基于一个或多个实际表（或其他视图）的查询结果而创建。视图提供了一种以某种特定方式查看数据的方法，而无需实际存储这些数据。视图的作用包括：

1. **数据过滤**：视图可以用于过滤数据，只显示满足特定条件的数据行。这有助于简化数据访问，并可以隐藏不必要的数据。

2. **数据转换**：视图可以用于对数据进行转换，例如合并多个表的数据，计算派生字段或进行数据格式转换。

3. **数据安全性**：通过视图，可以限制用户或应用程序对数据库中的特定数据的访问，而不必向他们提供对底层表的访问权限。

4. **简化查询**：视图可以将复杂的查询抽象为一个简单的视图，以便用户更轻松地检索所需的数据。

5. **逻辑数据独立性**：视图提供了逻辑数据模型与底层物理数据存储之间的隔离。这意味着视图的结构可以在不影响应用程序的情况下进行更改。

创建视图的语法如下：

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

- `CREATE VIEW`：用于创建视图的关键字。
- `view_name`：视图的名称。
- `AS`：用于指定视图的查询定义。
- `SELECT column1, column2, ...`：从一个或多个表中选择列以构建视图。
- `FROM table_name`：从哪个表中选择数据。
- `WHERE condition`：可选，用于定义过滤条件，以筛选要包括在视图中的行。

示例：

以下示例创建一个名为 "EmployeeNames" 的视图，该视图显示了来自 "Employees" 表的员工姓名：

```sql
CREATE VIEW EmployeeNames AS
SELECT FirstName, LastName
FROM Employees;
```

一旦视图创建，您可以像查询实际表一样查询视图。视图的数据是根据视图的查询定义实时生成的，它们不存储实际数据。视图提供了一种方便和安全的方式来访问和操作数据，尤其当需要简化数据访问和确保数据安全性时非常有用。



* 可以使用和表一样的操作形式,**最后的结果还是操作在原来的表上**



使用`DROP VIEW <view_name>`删除



# 第二次实验

* delete的时候不需要*



## 修改列名

在 SQL 查询中，您可以使用别名（Alias）来为一个列指定一个不同的名称，而不必更改实际表的列名。这对于在查询结果中更改列名非常有用，以便提供更具描述性的输出。您可以在 `SELECT` 语句中为列添加别名。

以下是如何在查询中为一个列添加别名的示例：

```sql
SELECT column_name AS alias_name
FROM table_name;
```

- `column_name`：要添加别名的列的实际名称。
- `alias_name`：您希望将列的别名设置为的名称。

示例：

假设有一个名为 "Students" 的表格，包括 "StudentID" 和 "FullName" 列，但您想在查询结果中将 "FullName" 列更改为 "StudentName"，可以这样做：

```sql
SELECT StudentID, FullName AS StudentName
FROM Students;
```

在查询结果中，"FullName" 列将显示为 "StudentName"，这是通过别名的方式实现的。这对于在查询结果中提供更清晰的列名称非常有用。



## 添加新的列名

要在 SQL 查询中添加一个新的列，您可以使用 `ALTER TABLE` 语句。这是一个示例 SQL 查询，说明如何添加一个新的列到现有表：

```sql
ALTER TABLE table_name
ADD new_column_name data_type;
```

在这个查询中：

- `table_name` 是您要添加新列的表的名称。
- `new_column_name` 是您要添加的新列的名称。
- `data_type` 是新列的数据类型，例如 `INT`（整数）、`VARCHAR(50)`（字符串，最大长度为 50 个字符）等。

示例：

假设您有一个名为 "Employees" 的表格，现在希望添加一个新的列 "Salary"，您可以执行以下 SQL 查询：

```sql
ALTER TABLE Employees
ADD Salary INT;
```

上述查询将在 "Employees" 表中添加一个名为 "Salary" 的整数列。新列将不包含任何数据，它只是一个新的列，您可以在后续查询中插入或更新数据。

请注意，您可以根据您的需求选择不同的数据类型和约束来定义新的列。数据库系统会根据定义的数据类型为新列分配合适的内存空间。





```sql
SELECT title,year,duration,'hrs' AS inhours
FROM(SELECT title,year,length/60 AS duration FROM movies)
```

> 是否**参数** AS **new coloumn name**的方式





## 查找date类型的值

在 PostgreSQL（pgsql）中，您可以使用类似的 SQL 查询来查找出生日期在七月的电影明星的姓名和出生日期。以下是 PostgreSQL 中的查询示例：

```sql
SELECT name, birthdate
FROM movie_stars
WHERE EXTRACT(MONTH FROM birthdate) = 7;
```

这个查询在 `movie_stars` 表中选择出生日期在七月的电影明星的姓名和出生日期。在 PostgreSQL 中，我们使用 `EXTRACT` 函数来提取日期的月份部分，并将其与 7 进行比较，以确定出生日期是否在七月。

确保表名和列名与您的数据库架构相匹配，以确保查询能够正确执行。



## 使用通配符

您可以使用 `LIKE` 操作符在 SQL 查询中进行模糊搜索，以查找与指定模式匹配的文本。`LIKE` 允许您在查询中使用通配符，如 `%` 和 `_`。

下面是如何使用 `LIKE` 来执行模糊搜索：

```sql
SELECT column_name
FROM table_name
WHERE column_name LIKE pattern;
```

- `column_name` 是您希望进行模糊搜索的列名。
- `table_name` 是包含该列的表名。
- `pattern` 是您希望匹配的模式。可以包含通配符。

通配符：

- `%`：匹配任意数量的字符（包括零个字符）。例如，`'a%'` 匹配以 'a' 开头的任何文本。
- `_`：匹配单个字符。例如，`'_pple'` 匹配任何以 'a' 开头，接着是一个字符，然后是 'pple' 的文本。

示例：

假设您有一个名为 "movies" 的表格，其中包括 "title" 列，您可以使用 `LIKE` 进行模糊搜索，查找包含特定文本的电影：

```sql
SELECT title
FROM movies
WHERE title LIKE '%Star%';
```

上述查询将返回包含 "Star" 的电影标题，无论 "Star" 在文本中的位置如何。



* 注意,通配符出现`'`的时候,需要使用两个`'`代表一个符号

```sql
SELECT * FROM movies
WHERE title LIKE '%''s%'
```



## 创建视图

在 SQL 中，您可以使用 `CREATE VIEW` 语句创建视图（View）。视图是虚拟的表，它是从一个或多个表中选择的行和列的查询结果，它本身并不存储数据，而只是一个可用于查询和报告的命名查询。以下是创建视图的一般语法：

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

- `view_name` 是您要创建的视图的名称。
- `column1, column2, ...` 是您要包括在视图中的列。
- `table_name` 是从中选择数据的表格。
- `condition`（可选）是用于筛选行的条件。

示例：

假设您有一个名为 "employees" 的表格，包括 "employee_id"、"first_name"、"last_name" 和 "salary" 列，您可以创建一个名为 "employee_view" 的视图，该视图只包括 "employee_id"、"first_name" 和 "salary" 列，如下所示：

```sql
CREATE VIEW employee_view AS
SELECT employee_id, first_name, salary
FROM employees;
```

此时，您已经创建了一个名为 "employee_view" 的视图，该视图包含了您在 `SELECT` 语句中指定的列。您可以像查询表一样查询视图，并从其中检索数据。

请注意，视图只是一个虚拟表，它基于基础表的数据。如果基础表中的数据发生更改，视图也会反映这些变化。视图通常用于简化复杂查询、限制对敏感数据的访问以及创建可重复使用的查询。



# aggregate function

* avg

> 会忽视null

```sql
select avg(networth)
from table
```



* total
* min
* max

> 也可以用在字符串(使用字典序),日期上

* count

> 统计有几个数值



tips

> 以上都会忽略null
>
> count可以使用*,其他是对准确的值操作
>
> 在一个值都没有的时候,count返回0,其他的返回null
>
> 可以对组聚类之后的数据操作.
>
> `trunc`取整

---



# order

> 排序使用(默认使用**升序**)

* 可以使用多个值来排序,有重要程度区分

```sql
select title 
from movies
where year<2000
order by studioname ,producerC desc
```

* 注意,这个desc只能作用于一个上面

* 可以对表上的原来的数据操作,也可以对组的数据操作.



# group by

```sql
select ...
from ..
where ..
group by ..
```

* 可以使用多个值来分组,只有当这些值都满足的时候,才是同一组.



> 因为一次分组,一组可以有多个值,所以,我们不能直接使用`select <原来的列名>`获取内容,需要使用`aggregate function`获取只有一个.

```sql
select studioname,count(*)
from table
group by studioname
```

> 使用名字分组,`count(*)`代表一组有几个数据



* 可以使用`order by`排序,需要放在后面.

* null被认为是同一个值,group value是正常的行数,但是计算单一个列的值的时候,会忽略null



# having

* `where`是对原来数据的内容做处理的,`having`是对分组之后的组做处理
* 不同的DBMS对having是否能在正常查询中使用不一样

`WHERE` 和 `HAVING` 是 SQL 中的两个关键字，它们都用于筛选数据。它们之间的区别在于：

- `WHERE` 关键字用于筛选行，而 `HAVING` 关键字用于筛选分组后的结果集。
- `WHERE` 关键字在 `GROUP BY` 分组和聚合函数之前执行，而 `HAVING` 关键字在 `GROUP BY` 分组和聚合函数之后执行。
- `WHERE` 关键字支持所有字段和运算符，而 `HAVING` 关键字主要支持组函数和运算符。

例如，假设我们有一个名为 `employees` 的表，其中包含员工的姓名、部门和薪水。如果我们想要找到薪水大于 5000 的员工，我们可以使用以下 SQL 查询：

```sql
SELECT * FROM employees WHERE salary > 5000;
```

如果我们想要找到每个部门的平均薪水大于 5000 的部门，我们可以使用以下 SQL 查询：

```sql
SELECT department, AVG(salary) FROM employees GROUP BY department HAVING AVG(salary) > 5000;
```



# 不等于

```sql
<>
```



# 第三次实验

使用`NOW()`获得现在的时间



# 多重查询(multirelation query)

从两个表R,S中查询数据



## 叉乘查询(join)

R*S

```sql
SELECT a,b,c
FROM table1,table2
```



* 如果两个表存在一样的**属性名字**,我们需要使用手动表明的方式

```sql
<relation>.<attribute>
```



### self join

可以作用在同一个的表上

* 起一个别名可以起到获得数据库表副本的方式



获得同一个住址的人

```sql
SELECT m1,name,m2.name
FROM moviestar m1,moviestar m2
WHERE m1.address=m2.address AND m1.name<m2.name
```

> 使用`<`,而不是`<>`.



获得比`Jane Fonda`年轻的人

```sql
select *
from moviestar m1,moviestar m2
where m1.name = 'Jane Fonda' AND m2.birhdate>m1.birthdate
```





## 表格合并

1. union

> 集合(不包含重复的内容,会自动去重)

```sql
(<表格一>)
union
(<表格二>)
```

* 属性名字由第一个表格中的属性名字决定



* 包括重复部分

> 使用`union all`



2. intersect

> 交集



3. except

> 在前一个数据表中存在,但是在后一个数据表中不存在的内容.



# subquery(子查询)

使用`WHERE`,`HAVING`实现

```sql
WHERE a = (select b from table)
```

* 获得一个属性值,比较子查询出来的一个属性值



* 如果子查询的返回值是null的时候,主要查询的值也是空.

* 如果子查询返回的值多于一个的时候,会报错.



## 关系关键词(在`WHERE`中)



`IN`

```sql
SELECT * FROM Customers WHERE CustomerID IN (SELECT CustomerID FROM Orders);
```

> 检测数据值是否存在在查询出来的数据表中

* 可以使用`WHERE (name,year) IN (...)`



`EXISTS`

```sql
SELECT * FROM Customers WHERE EXISTS (SELECT * FROM Orders WHERE Orders.CustomerID = Customers.CustomerID);
```

> 检测查询出来的值是否是非空的



在SQL中，**ALL**、**ANY**和**NOT**是用于比较值的逻辑操作符。

- **ALL**：用于比较一个值是否等于一组值中的所有值。例如，以下查询将返回所有价格高于所有产品的平均价格的产品：

  ```sql
  SELECT product_name
  FROM products
  WHERE price > ALL (
    SELECT AVG(price)
    FROM products
  );
  ```

* 直接使用`ANY`比较大小,可能会出现存在NULL值的情况,**所有和NULL比较的值结果都是NULL**.



- **ANY**：用于比较一个值是否等于一组值中的任何一个值。例如，以下查询将返回所有价格高于任何产品的平均价格的产品：

  ```sql
  SELECT product_name
  FROM products
  WHERE price > ANY (
    SELECT AVG(price)
    FROM products
  );
  ```

- **NOT**：用于否定一个条件。例如，以下查询将返回所有不是来自“德国”、“法国”或“英国”的客户：

  ```sql
  SELECT * FROM Customers WHERE Country NOT IN ('Germany', 'France', 'UK');
  ```

> 写在关键词的前面



* 使用`self subquery`的时候,也需要重新给表命名



## 子查询(在`FROM`中)



```sql
FROM movieexec,(SELECT * FROM movies WHERE ...) prod
```

> `prod`是重命名查询得到的表格的名字为`prod`.



# data control



## constrains(约束)

检查数据的合理性



1. catch data entry errors(捕获错误)
2. enforce consistency(保持相关数据统一)

> 可以实现多个表格之前的数据一致性



* not null
* keys
* check
* foreign-key(or referential-integrity) 相关



### NOT NULL

使用`NOT NULL`关键字

```sql
CREATE TABLE ... (
	gender CHAR(1) NOT NULL,
)
```



```sql
insert ...
values(null...)
```

不会允许



* 当使用UPDATE更新数据的时候,即使出现了NULL,如果没有找到需要被更新的值,那么也是不会报错的.



### KEY

使得一个或者多个属性值是独一无二的

* `UNIQUE`允许NULL数值

> 只允许出现多个NULL数值,NULL和所有的数值都是不相等的

* `PRIMARY KEY`不允许NULL



把多个值的组合作为一个KEY

```sql
CREATE TABLE ... (
	a int,
	b int,
    PRIMARY KEY(a,b)
)
```



### CHECK

把**check语句**写在属性的定义后面

```sql
gender CHAR(1) CHECK(gender IN ('F','M'))
```

> 这样写,可以允许插入NULL值



* `INSERT`和`UPDATE`的时候,都会执行CHECK



tuple check(多个数值组成)

```sql
CHECK (gender='F' OR name NOT LIKE 'Ms.%')
```



### REFERENTIAL INTEGRITY

使得一部分数据是相关的,可以自动更新

在一个表格中做的是**following key**

> from sub.A to main.B



使用`REFERENCES`语句

```sql
starname varchar(30) REFERENCES moviestar(name)
```

> 当你`insert`或者`update`SUB表格一个新的值的时候,如果,这个值不在`moviestar`表格的`name`中的时候,会报错.
>
> 使用`reference`的表格叫做`SUB`表格
>
> 被`reference`的表格叫做`MAIN`表格

> 可以随便往MAIN表格中添加新的内容,因为不受到`reference`限制
>
> **修改/删除**MAIN表格中的值,它可能会抛出错误,因为,它可能造成其他SUB表格的引用错误



* 注意,被`reference`的数值必须是`primary key`或者`unique`



### forgein key

tuple reference

```sql
foreign key(movietitle,movieyear) references movies(title,year)
```



reference模式

1. default

> 默认是不允许修改的

2. CASCADE

>  因为被引用之后,不可以在MAIN表格中自由修改属性值的问题

>  当一个值被修改的时候,可以自动修改`following value`.

3. SET NULL

> 设置为NULL

```sql
foreign key(starname) references movieestar(name)
on delete set null
on update cascade
```



## trigger

`event-[condition]-action rules`

当表格中执行一些操作的时候,执行对应的规则代码

> 如果一些SQL不支持一些语句,比如`CHECK`,可以使用trigger实现

```sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER | INSTEAD OF} {event}
ON table_name
[FOR [EACH] {ROW | STATEMENT}]
EXECUTE FUNCTION trigger_function();
```



> 使用`new`访问修改之后的值,使用`old`访问修改之前的值



步骤:

1. 创建一个触发器函数，该函数定义了要执行的操作。您可以使用`CREATE FUNCTION`语句创建触发器函数。触发器函数类似于普通的用户定义函数，但是它们不带参数并且返回类型为`trigger`。
2. 使用`CREATE TRIGGER`语句将触发器函数绑定到表上。您可以指定触发器应该在何时触发（例如，在插入、更新或删除行之前或之后），以及触发器应该与哪个表相关联。



# 实验5



## 创建一个触发器函数

```sql
CREATE FUNCTION update_movieexec_cert_function()
RETURNS TRIGGER AS
$$
BEGIN
	UPDATE studio
	SET studio.presC=studio.presC+(NEW.cert-OLD.cert)
	WHERE studio.presC=OLD.cert;
	RETURN NEW;
END;
$$
LANGUAGE plpgsql
```



## 创建一个触发器

```sql
CREATE TRIGGER update_movieexec_cert_trigger
AFTER UPDATE ON movieexec
FOR EACH ROW
EXECUTE FUNCTION update_movieexec_cert_function();
```



# transaction

处理同时的操作的



> [PGSQL的transation是指在数据库中执行一系列操作的一个逻辑单元。transation可以保证操作的原子性、一致性、隔离性和持久性，即ACID特性。transation可以用BEGIN或BEGIN TRANSACTION命令开始，用COMMIT或END TRANSACTION命令结束，或者用ROLLBACK命令撤销。transation可以用来处理复杂的业务逻辑，例如转账、购物等，以确保数据的完整性和安全性。](https://www.postgresql.org/docs/current/tutorial-transactions.html)[1](https://www.postgresql.org/docs/current/tutorial-transactions.html)[2](https://www.runoob.com/postgresql/postgresql-transaction.html)
>
> [1](https://www.postgresql.org/docs/current/tutorial-transactions.html): PostgreSQL: Documentation: 16: 3.4. [Transactions ](https://www.postgresql.org/docs/current/tutorial-transactions.html)[2](https://www.runoob.com/postgresql/postgresql-transaction.html): PostgreSQL TRANSACTION（事务） - 菜鸟教程



> many operations can be grouped into one group.
>
> many operations can be done automatically.



## ACID

atomicity 原子性

consistency 一致性

isolation 隔离性

durability 持久性

> [ACID特性是指**数据库**中的**事务**应该具备的四个特性，分别是**原子性**、**一致性**、**隔离性**和**持久性**。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)
>
> - [**原子性**（Atomicity）：事务中的所有操作要么全部成功，要么全部失败，不会出现部分完成的情况。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)
> - [**一致性**（Consistency）：事务的执行不会破坏数据库的完整性和一致性，事务前后数据库的状态都符合预设的规则。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)
> - [**隔离性**（Isolation）：事务之间不会相互影响，每个事务都是独立的，不会看到其他事务的中间结果。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)
> - [**持久性**（Durability）：事务一旦提交，其对数据库的修改就是永久的，即使发生系统故障或崩溃，也不会丢失数据。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)
>
> [ACID特性是保证数据库可靠性和正确性的重要原则，也是区分关系型数据库和非关系型数据库的一个标准。](https://it-biz.online/it-skills/acid/)[1](https://it-biz.online/it-skills/acid/)[2](https://e-words.jp/w/ACID特性.html)[3](https://blog.trocco.io/glossary/acid)



## 隔离等级

隔离等级是指数据库在并发事务处理时，对事务之间的可见性和影响程度的控制。不同的隔离等级有不同的性能和一致性的权衡。SQL标准定义了四种隔离等级，分别是：

- **读未提交**（Read Uncommitted）：最低的隔离等级，允许事务读取未提交的数据，可能导致脏读、不可重复读和幻读的问题。
- **读已提交**（Read Committed）：只允许事务读取已提交的数据，避免了脏读的问题，但是可能出现不可重复读和幻读的问题。
- **可重复读**（Repeatable Read）：保证事务在同一时间读取的数据是一致的，避免了脏读和不可重复读的问题，但是可能出现幻读的问题。这是MySQL的默认隔离等级。
- **串行化**（Serializable）：最高的隔离等级，要求事务串行执行，避免了所有的并发问题，但是性能最差。



脏读(dirty read): 读到了未被提交并且执行失败被回滚的数据.(在**read uncommitted**中会出现 	)

> 可以使用**read committed**来避免



如果重复查询一个值,这个值被多次查询前后经过了commit,那么,读到的值依旧会发生改变

我们希望再自己多次查询的commit之前,查询的数值也不发生改变

> 使用**repeatable read**



# E/R(entity / relationship)

entity / relationship diagrams



## entity

一个现实中的物体实体



* 多个实体构成entity set



### entity attribute

属性,一个个数值



## 画E/R diagrams

the entity is a reactangle

the entity attribute is a oval

实体之间的关系(relation),使用**线和菱形(diamond)**链接



1. 把entity set放到一个图表里面去

* 一个实体本身也是一个relationship,relationship的个数 = realtion(菱形的个数) + entity(实体的个数)



# convert diagram to relational scheme

1. 图中的每个element(entity)作为一个表格
2. element之间的连接应该被作为一个新的relation

* 使用**连接两个entity构成的新的表格**不需要包含elements的全部内容(只需要key attributes)
* 如果存在`many-one`(一个element的一个主键可以关联另一个表格中的多个),并且,另一个表格的主键和新表格的主键一一对应,那么可以合并新的表格和一一对应的表格



## multipicity

* `many-one`: 多对一的关系
* `one-one`: 一对一的关系
* `many-many`: 多对多的关系



### many-one

**使用一个箭头指向`one`的部分**,代表非箭头的部分(many)可以使用至多一个`one`部分的元素.

> arrow: at most one(至多一个)
>
> round arrow: exactly one(有且仅有一个)



## 合并表格

出现`many-one`的关系的时候,可以使用**`many`的部分和要构建出的新relation**合并

> `many`部分中的全部属性 + `one`部分的key attributes



* 你可以从**合并的表格**中抽取key attributes作为**原本新增的relation**.



### supporting entity set

如果一个entity是supporting entity set,需要满足

> 1. 是`many-one`关系中的`one`部分
> 2. 不适用合并表格的话,`many`部分会有重复(不能正常使用key attributes)



* 使用**double diamond(2倍轮廓线的菱形)**表示relationship



### weak entity set

与上述supporting entity set相关



* 使用**double reactangle(两倍矩形)**表示weak entity set



## super class

superclass and subclass is connected by relationship called isa



* 使用**triangle(三角形) + 线**表示super class和sub class的连接



* superclass需要包含subclass的全部数据内容



## subclass

![image-20231222120135626](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20231222120135626.png)

> 尖端指向的部分是super class
>
> 平面指的是subclass



子类不需要包含superclass中的全部属性,只需要包含**superclass的key attributes和自己的特有的属性**.

> 获取的具体数据的时候,会使用key attributes到superclass中查找



# normalization

redundant information : 不必要的信息

update anomalies : 修改异常

deletion anomalies : 删除异常



# decompose

避免anomalies的出现

> 正确的拆分entity set的内容



* key attributes需要一致



## 第一级别的设计

> 全部的属性全部放到一个entity set中



## super key

包含key attributes,同时也可能包含其他内容



> key: title,year
>
> super key: title,year,length



## functional dependence

多个值的对应的值是唯一的



### trival functional dependence

琐碎的FD

> key组成的集合可以确定其中任意一个key的内容



### super key

使用key组成的集合可以确定任何一个非key attribute



* 有些时候,部分的key就可以表达其他的值,说明key多余了,不属于第二级设计



## 第二级的设计

non-key attribute is not partly functionally dependent on the primary key



步骤

> 1. 确定key attributes



* 如果只有一个key,那么它一定是第二级的设计,因为一个key不可以再被拆分了



## 第三级的设计

第二级的设计可能出现,non-key可以被non-key functional dependent

我们需要尽量避免出现non-key can be determined by another non-key



## BCNF(boyce-codd normal form)

步骤

> 1. decide the key(找到所有的KEY)
> 2. work out all nontrival FD



* 左边的式子需要是super key



## 第四级的设计

multivalued dependency



# 复习



## 定义一个数据库

![image-20240105174745489](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240105174745489.png)





## 创建一个表

![image-20240105175851083](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240105175851083.png)



`CHAR(n)`指的是具体n个的字符串

`VARCHAR(n)`指的是至多n个的字符串



## 删除一个表

`DROP TABLE R;`



## 数据库系统的标准结构

external level = user level 

conceptual level = logic level

internal level = physical level



## TIP

relation = table



## types of data model

* hierarchical data model : like a tree
* graph data model : like the graph
* relational data model : use data structure as a set of tables
* object-oriented data model
* object relational data model
* semi-structure data model 
* nosql data model



## data structure

table and only table



it is a logical structure instead of physical structure, 从物理的底层存储中抽象出来了一种表示



## 行定义

attributes : header row

tuple : a row beside the header row/an ordered list of vale



## schemas

relation schema = relation name(attribute list)



## TIP

行.列的顺序不重要,tuple and attributes一样就是同一张表



database = set of named realtions/tables

each realtion has a set of named attributes/columns

each tuple/row has a value for each attribute

each attribute has a type/domain

database schema = relation schema sets



## modification

insert a tuple or tuples

delete a tuple or tuples

update the value(s) of an existing tuples



## basic integrity in relational database

* no tuples are absolutely same(没有绝对相同的数据)
* no attributes titles are absolutely same in one table(没有属性名是相同的)

* there should be a primary key(但不是绝对要求有主键)



## key

attribute whose value is unique in each tuple

* 存在联合键,多个属性构成一个key

* 



使用下划线标注作为key的属性



设置primary key

`name VARCHAR(255) PRIMARY KEY`



## unique

可以使用这个关键字设置attribute value是不同的



* unique运行null,但是primary key不允许null(注意,全部的primary key字段都不能为null)



## alter 修改表

添加一个attribute

```sql
ALTER TABLE R 
ADD attribute_name attribute_type;
```



删除一个attribute

```sql
ALTER TABLE R 
DROP attribute_name;
```



## 12 rules

1. the data stored in database must e a value of some table cell
2. very single data element need to be accessiable with a combination of table name, attribute name primary key
3. null value needs to be treated specially
4. activate online catalog
5. the database can be only accessed by the lanuage
6. the database can be updated must also be updatable by the system
7. 



## operator in relational algebra

![image-20240106145849262](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106145849262.png)



![image-20240106152045420](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106152045420.png)



![image-20240106152710146](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106152710146.png)



![image-20240106153354050](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106153354050.png)



![image-20240106153921947](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106153921947.png)



* 如果在natural join之前进行renaming,可以方便的合并





![image-20240106155205790](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106155205790.png)

![image-20240106155400714](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106155400714.png)

![image-20240106155550054](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106155550054.png)

![image-20240106155657217](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106155657217.png)

例题

![image-20240106160245792](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106160245792.png)

![image-20240106160300916](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106160300916.png)



## SQL语句的类别

![image-20240106160553352](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106160553352.png)



## 查询语句

```sql
SELECT name,address
FROM table_name
WHERE condition;
```



### 查询到的语句输出常量

![image-20240106190214237](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106190214237.png)

> 会多出一个全都是`hours`的列



### 查询的时候使用新的列名

If you want the result to have different attribute names, use  “AS ” to rename an attribute.

```sql
SELECT title,year,length/60 as duration,’hours’ as inhours
FROM movies;
```



## NULL

用来表示丢失或者不存在的值

* 使用比较的时候,会出现**unkown**
* 可以使用**IS**/**IS NOT**检查



## logic of conditions

1. true
2. false
3. unkown



![image-20240106192803826](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106192803826.png)

![image-20240106192931381](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106192931381.png)



## 使用`BETWEEN AND`

```sql
SELECT title,year,length
FROM movie
WhERE length BETWEEN 116 AND 120;
```



## LIKE

通配符包括`%`,`_`



`%` ( = “any string”);  

`_` ( = “any character.”);



* 可以使用`NOT LIKE`排除一种状况



## VIEW

[pgsql 的 view（视图）是一种虚拟的表，它是由一个预定义的查询语句生成的。视图不会实际存储数据，而是每次引用时执行查询语句。视图可以从一个或多个表或其他视图创建，它可以让用户以更自然或直观的方式查看数据，也可以限制数据的访问，或者汇总多个表的数据](https://www.postgresql.org/docs/current/sql-createview.html)[1](https://www.postgresql.org/docs/current/sql-createview.html)[2](https://www.runoob.com/postgresql/postgresql-view.html)。



创建一个视图

```sql
create View Vname As
<Query>
```

```sql
Create View(A1…An) Vname As
<Query>
```



* 插入删除修改数据的操作和TABLE是一样的



## 排序

```sql
SELECT * FROM weather ORDER BY city ASC, temp_lo DESC;
```



## aggregation operator(聚合操作)

包含sum ,Avg,max,min,count

> Sql use five aggregation operators to calculate result  from set of values .



```sql
SELECT avg(length)
FROM movies
```



[pgsql 的 aggregation operator（聚合操作符）是一种用于对一组值进行计算并返回一个单一结果的函数，例如 sum, avg, count, max, min 等](https://www.postgresql.org/docs/current/functions-aggregate.html)[1](https://www.postgresql.org/docs/current/functions-aggregate.html)。pgsql 的聚合操作符对 NULL 的操作会根据不同的函数而有不同的结果，一般来说，有以下几种情况：

- [如果聚合操作符的输入值都是 NULL，那么返回值也是 NULL。例如，`sum(NULL)` 返回 NULL](https://blog.csdn.net/djrm11/article/details/118210285)[2](https://blog.csdn.net/djrm11/article/details/118210285)。
- [如果聚合操作符的输入值中有 NULL 和非 NULL 的混合，那么返回值会忽略 NULL 并只计算非 NULL 的值。例如，`avg(1, 2, NULL, 4)` 返回 2.333](https://blog.csdn.net/djrm11/article/details/118210285)[2](https://blog.csdn.net/djrm11/article/details/118210285)。
- [如果聚合操作符的输入值中有 NULL 和非 NULL 的混合，但是要求返回值不能为 NULL，那么可以使用 COALESCE 函数来替换 NULL 为其他值。例如，`sum(COALESCE(salary, 0))` 可以将 salary 列中的 NULL 替换为 0，然后计算总和](https://bbs.csdn.net/topics/190179836)[3](https://bbs.csdn.net/topics/190179836)。



### COUNT计算NULL值

pgsql 中，COUNT 计数的列如果遇到 NULL 会怎么样，取决于 COUNT 的用法。一般来说，有以下两种情况：

- [如果使用 COUNT (*)，那么会计算表中的所有行，不管是否包含 NULL 值](https://www.cnblogs.com/gered/p/12195729.html)[1](https://www.cnblogs.com/gered/p/12195729.html)[2](https://zhuanlan.zhihu.com/p/538688824)。例如，`SELECT COUNT (*) FROM test;` 会返回 test 表中的总行数，不管每一行的值是否为 NULL。
- [如果使用 COUNT (列名)，那么会忽略 NULL 值，只计算非 NULL 值的行](https://www.cnblogs.com/gered/p/12195729.html)[1](https://www.cnblogs.com/gered/p/12195729.html)[2](https://zhuanlan.zhihu.com/p/538688824)。例如，`SELECT COUNT (name) FROM test;` 会返回 test 表中 name 列的非 NULL 值的行数，如果 name 列的值都是 NULL，那么结果为 0。



## GROUP BY(分组)

可以根据莫一个列来分组

```sql
select studioname
from movies
group by studioname;
```



* 在分组的状态下使用



## HAVING

用来筛选group

```sql
Select A1,A2,…,An
From R1
Where condition
Group by Ak
Having condition 
Order by Ai [ASC|DESC], Aj [ASC|DESC], …
```



* 注意,`GROUP BY ... HAVING ...`要在`ORDER BY`之前 



## DISTINCT

- SELECT DISTINCT：在返回查询结果之前，去除重复的记录，每个重复的数据组中只保留一条记录。例如，`SELECT DISTINCT name FROM employee;` 会返回 employee 表中的所有不同的姓名。
- DISTINCT ON：根据指定的列或表达式，返回每个分组中的第一条记录。例如，`SELECT DISTINCT ON (dept_id) dept_id, name, salary FROM employee ORDER BY dept_id, salary DESC;` 会返回每个部门中薪水最高的员工的信息。
- IS DISTINCT FROM：用于比较两个可能为空的值是否不同。例如，`SELECT 1 IS DISTINCT FROM NULL;` 会返回 true，而 `SELECT NULL IS DISTINCT FROM NULL;` 会返回 false。
- 聚合函数中的 DISTINCT：用于对一组值进行计算时，只考虑不重复的值。例如，`SELECT COUNT(DISTINCT name) FROM employee;` 会返回 employee 表中的不同姓名的个数。



## CONCAT

用来合并字符串

```sql
select title,year,concat(length/60,"hrs")
from movies
```



## EXTRACT

从数据中提取一部分的内容

```sql
Select Name,extract(year from birthdate)as birthyear
From moviestar
```



[pgsql 的 EXTRACT 是一种函数，它可以从日期或时间值中提取出指定的字段，例如年、月、日、时、分、秒等](https://www.rockdata.net/zh-cn/tutorial/function-extract/)[1](https://www.rockdata.net/zh-cn/tutorial/function-extract/)。它的语法如下：

```sql
EXTRACT(field FROM source)
```

[其中，field 是要提取的字段，可以是以下值之一](https://www.rockdata.net/zh-cn/tutorial/function-extract/)[2](https://www.postgresql.org/docs/current/functions-datetime.html)：

- YEAR
- MONTH
- DAY
- HOUR
- MINUTE
- SECOND
- CENTURY
- DECADE
- DOW
- DOY
- EPOCH
- ISODOW
- ISOYEAR
- MICROSECONDS
- MILLISECONDS
- QUARTER
- TIMEZONE
- TIMEZONE_HOUR
- TIMEZONE_MINUTE
- WEEK

[source 是要提取的日期或时间值，可以是 TIMESTAMP, TIME, INTERVAL, 或 DATE 类型的值或表达式](https://www.rockdata.net/zh-cn/tutorial/function-extract/)[1](https://www.rockdata.net/zh-cn/tutorial/function-extract/)。

例如，以下是一些使用 EXTRACT 的示例：

- 从 TIMESTAMP 值中提取年份：

```sql
SELECT EXTRACT(YEAR FROM TIMESTAMP '2021-04-06 12:43:59');
```

结果是 2021。

- 从 TIME 值中提取分钟部分：

```sql
SELECT EXTRACT(MINUTE FROM TIME '12:43:59');
```

结果是 43。

- 从 INTERVAL 值中提取秒数部分：

```sql
SELECT EXTRACT(SECOND FROM INTERVAL '6 years 5 months 4 days 3 hours 2 minutes 1 second');
```

结果是 1。

- 从 DATE 值中提取一年中的第几天：

```sql
SELECT EXTRACT(DOY FROM DATE '2021-04-06');
```

结果是 96。



## join

![image-20240106213517716](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240106213517716.png)



### self-join

* Select statement allow working on same relations
* In order to distinguish, give each relation an alias

```sql
SELECR r1.A1,…,r1.An ,r2.A1……
FROM R r1 , R r2
WHERE condition
```

**注意,在这里不需要使用`AS`关键词**

**注意,我们使用self-join的时候,一般会使用`>`/`<`运算符,防止数据重复**



例题

>  Find the star pairs that share the same address

```sql
SELECR star1.name,star2.name,star2.address
FROM moviestar star1,moviestar star2
WHERE star1.name<star2.name AND 
star1.address=star2.address
```



## 集合操作

![image-20240107120300478](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107120300478.png)



## subquery with WHERE

注意,子查询需要使用`()`包含.

* Subqueries can return a single constant , and  this constant can be compared with another  value in a WHERE clause

![image-20240107121744921](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107121744921.png)



### subquery的操作符

PGSQL的子查询操作符是用于在一个查询中嵌入另一个查询的方法。子查询操作符可以用于比较表达式、逻辑表达式或集合表达式中。PGSQL支持以下几种子查询操作符：

- **EXISTS**：判断子查询是否返回至少一行数据。如果是，返回true，否则返回false。例如：

```
SELECT col1 FROM tab1 WHERE EXISTS (SELECT 1 FROM tab2 WHERE col2 = tab1.col2);
```

- **IN**：判断一个值是否在子查询返回的集合中。如果是，返回true，否则返回false。例如：

```
SELECT film_id, title FROM film WHERE film_id IN (SELECT inventory.film_id FROM rental);
```

- **ANY / SOME**：判断一个值是否满足子查询返回的集合中的任意一个或某些元素的条件。如果是，返回true，否则返回false。例如：

```
SELECT film_id, title FROM film WHERE rental_rate > ANY (SELECT rental_rate FROM film WHERE rating = 'R');
```

- **ALL**：判断一个值是否满足子查询返回的集合中的所有元素的条件。如果是，返回true，否则返回false。例如：

```
SELECT film_id, title FROM film WHERE rental_rate < ALL (SELECT rental_rate FROM film WHERE rating = 'G');
```

* **NOT**



### 当子查询中不仅仅包含一个attribute的时候

![image-20240107123922648](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107123922648.png)



## subquery with FROM



*  We need a name for referring to the relation computed  by the subqueries(所以,我们需要在FROM语句中给查询出来的内容起名)



## constraints

A constraint is a relationship among data  elements that the DBMS is required to  enforce.



[PGSQL的约束是用于规定表中的数据规则的一种方法。如果存在违反约束的数据行为，行为会被约束终止。约束可以在创建表时规定，也可以在表创建之后规定。约束确保了数据库中数据的准确性和可靠性。](https://www.postgresql.org/docs/current/ddl-constraints.html)[1](https://www.postgresql.org/docs/current/ddl-constraints.html)

PGSQL支持以下几种约束：

- **NOT NULL**：指示某列不能存储NULL值。
- **UNIQUE**：确保某列的值都是唯一的。
- **PRIMARY KEY**：NOT NULL和UNIQUE的结合。确保某列（或多个列的组合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
- **FOREIGN KEY**：保证一个表中的数据匹配另一个表中的值的参照完整性。

```sql
presC int references movieexec(cert)
```

> referenced attributes must be defined as primary key or unique

```sql
CREATE TABLE comment (
  name varchar(45),
  owner varchar(45),
  id uuid,
  comment text,
  PRIMARY KEY (id),
  CONSTRAINT comment_name_fkey
    FOREIGN KEY (name, owner)
    REFERENCES cat (name, owner)
);
```





- **CHECK**：保证列中的值符合指定的条件。
- **EXCLUSION**：排他约束，保证如果将任何两行的指定列或表达式使用指定操作符进行比较，至少其中一个操作符比较将会返回false或空值。



### 不满足的时候执行的操作

![image-20240107142524468](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107142524468.png)



## CHECK

在**插入/更新**数据的时候执行



```sql
Gender CHAR(1) CHECK(gender IN ('F', ‘M'))
```



```sql
CREATE TABLE moviestar (
name varCHAR(30) primary key,
address varCHAR(255),
gender char(1),
birthdate DATE,
CHECK (gender=’F’ OR name not like ’Ms.%’ );
```



## TRIGGER

![image-20240107145909714](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107145909714.png)

* 注意,`old`和`new`都是对修改的那个数据的



## VIEW



### 类别

1. Virtual = not stored in the database; just a  query for constructing the relation.
2. Materialized = actually constructed and  stored.



## INDEX

![image-20240107153333252](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107153333252.png)

> 使用B-树加快搜索



## ER

entity : 一个实体, a tuple of table

entity : 实体集合

entity attribute



### ER图形状

Entity set = rectangle

Attribute = oval, with a line to the rectangle representing its  entity set.

relationship = diamond



* relationship图中只有组成图中的主键



## MULTIPLICITY



many-one

![image-20240107160820549](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107160820549.png)

![image-20240107160834068](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107160834068.png)



* 可以合并relationship和table

![image-20240107161519830](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107161519830.png)



one-one

![image-20240107160903721](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107160903721.png)



superclass/subclass

![image-20240107163800694](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240107163800694.png)



## redundant

可能造成

1. 修改一个内容的时候,其他数据中的相同内容没有被修改 UPDATE ANOMALIES
2. 删除的时候,可能删除过多的内容 DELETION ANOMALIES

使用DECOMPOSE



## 1ST NORMAL FORM

![image-20240108150610690](C:\Users\Thinkpad\AppData\Roaming\Typora\typora-user-images\image-20240108150610690.png)
