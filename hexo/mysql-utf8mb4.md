---
title: MySQL-更改MySQL默认编码为utf8mb4
date: 2017-05-13
description: "让应用程序支持emoji字符"
categories: [MySQL]
tags: [MySQL, Database]
---

`utf8mb4`是`utf8`的超集，emoji表情以及部分不常见汉字在utf8下会表现为乱码,故需要升级至`utf8mb4`.

如果使用MySQL作为数据库，需要升级到5.5.3或更新的版本，然后，把默认编码从原来的`utf8`改为`utf8mb4`.
找到MySQL配置文件:
```shell
find / -name "my.cnf"
```

在`my.cnf`或者`my.ini`配置文件中修改如下：
```mysql
[client]
default-character-set = utf8mb4

[mysqld]
character_set_server=utf8mb4
init_connect='SET NAMES utf8mb4'
collation-server=utf8mb4_general_ci
```

重启MySQL，然后使用以下命令查看编码，应该全部为`utf8mb4`（`character_set_filesystem`和`character_set_system`除外）：
```mysql
mysql> show variables like '%char%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8mb4                    |
| character_set_connection | utf8mb4                    |
| character_set_database   | utf8mb4                    |
| character_set_filesystem | binary                     |
| character_set_results    | utf8mb4                    |
| character_set_server     | utf8mb4                    |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.00 sec)
```

使用命令查看collation设置，应该全部是 `utf8mb4_general_ci`：
```mysql
mysql>  show variables like '%coll%';
+----------------------+--------------------+
| Variable_name        | Value              |
+----------------------+--------------------+
| collation_connection | utf8mb4_general_ci |
| collation_database   | utf8mb4_general_ci |
| collation_server     | utf8mb4_general_ci |
+----------------------+--------------------+
3 rows in set (0.00 sec)
```
---
参考: 
廖雪峰的官方网站-[让应用程序支持emoji字符][1]
[MySQL 5.7 Reference Manual][2]

[1]:http://www.liaoxuefeng.com/article/00145803336427519ae82a6c5b5474682c0c4ba5b47fb33000
[2]:https://dev.mysql.com/doc/refman/5.7/en/