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
