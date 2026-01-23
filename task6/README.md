Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 48
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> create table employees(
    -> emp_id int primary key,
    -> emp_name varchar(50),
    -> department varchar(30),
    -> salary int,
    -> email varchar(50)
    -> );
Query OK, 0 rows affected (1.501 sec)

mysql> desc employees;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| emp_id     | int         | NO   | PRI | NULL    |       |
| emp_name   | varchar(50) | YES  |     | NULL    |       |
| department | varchar(30) | YES  |     | NULL    |       |
| salary     | int         | YES  |     | NULL    |       |
| email      | varchar(50) | YES  |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
5 rows in set (0.736 sec)

mysql> insert into employees values
    -> (1,'ravi','it',40000,'ravi@gmail.com'),
    -> (2,'sita','HR',35000,'sita@gmail.com'),
    -> (3,'keechu','IT',45000,'keechu@gmail.com'),
    -> (4,'anu','Finance',30000,NULL),
    -> (5,'vamsi','HR',38000,'vamsi@gmail.com');
Query OK, 5 rows affected (0.551 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select*from employees;
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      2 | sita     | HR         |  35000 | sita@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
|      4 | anu      | Finance    |  30000 | NULL             |
|      5 | vamsi    | HR         |  38000 | vamsi@gmail.com  |
+--------+----------+------------+--------+------------------+
5 rows in set (0.012 sec)

mysql> select*from employees where department='IT';
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
+--------+----------+------------+--------+------------------+
2 rows in set (0.393 sec)

mysql> select*from employees where salary>35000;
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
|      5 | vamsi    | HR         |  38000 | vamsi@gmail.com  |
+--------+----------+------------+--------+------------------+
3 rows in set (0.011 sec)

mysql> update employees set salary=salary+2000 where department='HR';
Query OK, 2 rows affected (0.518 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> select*from employees;
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      2 | sita     | HR         |  37000 | sita@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
|      4 | anu      | Finance    |  30000 | NULL             |
|      5 | vamsi    | HR         |  40000 | vamsi@gmail.com  |
+--------+----------+------------+--------+------------------+
5 rows in set (0.010 sec)

mysql> delete from employees where emp_id=4;
Query OK, 1 row affected (0.087 sec)

mysql> select*from employees where department='Finance';
Empty set (0.012 sec)

mysql> delete from employees where department='finance';
Query OK, 0 rows affected (0.010 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.390 sec)

mysql> delete from employees where emp_id=5;
Query OK, 1 row affected (0.013 sec)

mysql> rollback;
Query OK, 0 rows affected (0.481 sec)

mysql> select*from employees;
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      2 | sita     | HR         |  37000 | sita@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
|      5 | vamsi    | HR         |  40000 | vamsi@gmail.com  |
+--------+----------+------------+--------+------------------+
4 rows in set (0.010 sec)

mysql> select*from employees;
+--------+----------+------------+--------+------------------+
| emp_id | emp_name | department | salary | email            |
+--------+----------+------------+--------+------------------+
|      1 | ravi     | it         |  40000 | ravi@gmail.com   |
|      2 | sita     | HR         |  37000 | sita@gmail.com   |
|      3 | keechu   | IT         |  45000 | keechu@gmail.com |
|      5 | vamsi    | HR         |  40000 | vamsi@gmail.com  |
+--------+----------+------------+--------+------------------+
4 rows in set (0.010 sec)

mysql>










