Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 37
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> create database intern_training_db;
Query OK, 1 row affected (0.537 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| intern_training_db |
| keerthi            |
| mysql              |
| pavani             |
| performance_schema |
| sys                |
+--------------------+
7 rows in set (0.023 sec)

mysql> use intern_training_db;
Database changed
mysql> create table students(
    -> id INT PRIMARY KEY,
    -> name VARCHAR(50),
    -> email VARCHAR(50),
    -> age INT
    -> );
Query OK, 0 rows affected (0.684 sec)

mysql> show tables;
+------------------------------+
| Tables_in_intern_training_db |
+------------------------------+
| students                     |
+------------------------------+
1 row in set (0.033 sec)

mysql> insert into students values(1,'priya','priya@gmail.com',19);
Query OK, 1 row affected (0.514 sec)

mysql> insert into students values(2,'divya','divya@gmail.com',20);
Query OK, 1 row affected (0.443 sec)

mysql> insert into students values(3,'manju','manju@gmail.com',20);
Query OK, 1 row affected (0.075 sec)

mysql> insert into students values(4,'keerthi','keechu@gmail.com',19);
Query OK, 1 row affected (0.067 sec)

mysql> insert into students values(5,'venu','venu@gmail.com',21);
Query OK, 1 row affected (0.772 sec)

mysql> select*from students;
+----+---------+------------------+------+
| id | name    | email            | age  |
+----+---------+------------------+------+
|  1 | priya   | priya@gmail.com  |   19 |
|  2 | divya   | divya@gmail.com  |   20 |
|  3 | manju   | manju@gmail.com  |   20 |
|  4 | keerthi | keechu@gmail.com |   19 |
|  5 | venu    | venu@gmail.com   |   21 |
+----+---------+------------------+------+
5 rows in set (0.010 sec)

mysql> select name,email from students;
+---------+------------------+
| name    | email            |
+---------+------------------+
| priya   | priya@gmail.com  |
| divya   | divya@gmail.com  |
| manju   | manju@gmail.com  |
| keerthi | keechu@gmail.com |
| venu    | venu@gmail.com   |
+---------+------------------+
5 rows in set (0.011 sec)

mysql> select name,age from students;
+---------+------+
| name    | age  |
+---------+------+
| priya   |   19 |
| divya   |   20 |
| manju   |   20 |
| keerthi |   19 |
| venu    |   21 |
+---------+------+
5 rows in set (0.010 sec)

mysql> select name,age from students where age>20;
+------+------+
| name | age  |
+------+------+
| venu |   21 |
+------+------+
1 row in set (0.081 sec)

mysql> insert into students values(6,'prasu','prasu@gmail.com',21);
Query OK, 1 row affected (0.519 sec)

mysql> select*from students;
+----+---------+------------------+------+
| id | name    | email            | age  |
+----+---------+------------------+------+
|  1 | priya   | priya@gmail.com  |   19 |
|  2 | divya   | divya@gmail.com  |   20 |
|  3 | manju   | manju@gmail.com  |   20 |
|  4 | keerthi | keechu@gmail.com |   19 |
|  5 | venu    | venu@gmail.com   |   21 |
|  6 | prasu   | prasu@gmail.com  |   21 |
+----+---------+------------------+------+
6 rows in set (0.010 sec)

mysql> update students set age=22 where id=3;
Query OK, 1 row affected (0.458 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select*from students where id=3;
+----+-------+-----------------+------+
| id | name  | email           | age  |
+----+-------+-----------------+------+
|  3 | manju | manju@gmail.com |   22 |
+----+-------+-----------------+------+
1 row in set (0.011 sec)

mysql> delete from students where id=2;
Query OK, 1 row affected (0.579 sec)

mysql> select*from students;
+----+---------+------------------+------+
| id | name    | email            | age  |
+----+---------+------------------+------+
|  1 | priya   | priya@gmail.com  |   19 |
|  3 | manju   | manju@gmail.com  |   22 |
|  4 | keerthi | keechu@gmail.com |   19 |
|  5 | venu    | venu@gmail.com   |   21 |
|  6 | prasu   | prasu@gmail.com  |   21 |
+----+---------+------------------+------+
5 rows in set (0.010 sec)

mysql>













