# Mysql 与 C/C++

本篇介绍 `Windows` `Mysql` 与 `C/C++` 开发的命令行连接方法。



## 编译

* 将 `Mysql` 安装目录下的 `include文件夹` 拷贝到工程目录。

* 拷贝 `libmysql.dll`、`libcrypto-1_1-x64.dll`、`libssl-1_1-x64.dll` 到工程目录。

* 编译命令为

  ``` bash
  g++ main.cpp -o main -I include -L . -l mysql
  ```

* `dll` 动态库必须位于工程根目录，不得重命名。（因为我不会其他方法）



## 接口

### GET START

因为偷懒，这里只有 `GET START` ，仔细看相信大家都能看懂。

``` cpp
#include <bits/stdc++.h>
#include "mysql.h"
using namespace std;

MYSQL mysql;  // Mysql 结构体
MYSQL_RES *mysql_res;  // 返回结果集
MYSQL_ROW mysql_row;  // 暂存单行记录
 
// 假设服务端口为：	root@localhost:3306 jamhus_tao
// 假设已创建数据库：CREATE DATABASE school CHARSET gbk;
// 假设数据库已建表：CREATE TABLE score(ID int, name varchar(255), age int, score int, PRIMARY KEY(ID));

// 查询全部数据并输出
void display() {
	// 查询数据，此处可以传递任何 SQL 语句，操作量大时不建议直接使用临时字符串传递
	int ret = mysql_query(&mysql, "SELECT * FROM score;");

    if (ret) {
        // 输出错误信息，当 ret 返回 1 表示错误时
		cout << mysql_error(&mysql) << endl;
    }

	// 获取结果集，捕捉 mysql_query 输出的数据
	res = mysql_store_result(&mysql);  

	cout << "ID  name  age  score" << endl;
    // 给 ROW 赋值，判断 ROW 是否为空，不为空就打印数据。
	while (row = mysql_fetch_row(res)) {
		cout << row[0] << "  ";  // 打印 ID
		cout << row[1] << "  ";  // 打印 name
		cout << row[2] << "  ";  // 打印 age
		cout << row[3] << endl;  // 打印 score
	}

	// 释放结果集，每次获取结果集后都要释放
	mysql_free_result(res);
}

int main() {
	// 初始化数据库
	mysql_init(&mysql);

	// 设置字符编码
	mysql_options(&mysql, MYSQL_SET_CHARSET_NAME, "gbk");

	// 连接数据库
    // localhost 为服务器，root 为用户名和密码，school 为数据库名，3306 为端口
	if (mysql_real_connect(&mysql, "localhost", "root", "root", "school", 3306, NULL, 0) == NULL) {
        cout << "连接失败！" << endl;
        cout << "错误代码：" << mysql_errno(&mysql) << endl;
        cout << "错误原因：" << mysql_error(&mysql) << endl;
		exit(-1);
	}

    display();

    //关闭数据库
	mysql_close(&mysql);
	return 0;
}
```

