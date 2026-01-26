Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> create table departments(
    -> department_id int primary key,
    -> department_name varchar(50)
    -> );
Query OK, 0 rows affected (0.273 sec)

mysql> desc departments;
+-----------------+-------------+------+-----+---------+-------+
| Field           | Type        | Null | Key | Default | Extra |
+-----------------+-------------+------+-----+---------+-------+
| department_id   | int         | NO   | PRI | NULL    |       |
| department_name | varchar(50) | YES  |     | NULL    |       |
+-----------------+-------------+------+-----+---------+-------+
2 rows in set (0.037 sec)

mysql> create table employees(
    -> emp_id int primary key,
    -> emp_name varchar(50),
    -> department_id int,
    -> salary int,
    -> foreign key(department_id) references departments(department_id)
    -> );
Query OK, 0 rows affected (2.332 sec)

mysql> desc employees;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| emp_id        | int         | NO   | PRI | NULL    |       |
| emp_name      | varchar(50) | YES  |     | NULL    |       |
| department_id | int         | YES  | MUL | NULL    |       |
| salary        | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.030 sec)

mysql> insert into departments values
    -> (1,'IT'),
    -> (2,'HR'),
    -> (3,'Finance');
Query OK, 3 rows affected (0.476 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> insert into employees values
    -> (101,'ravi',1,40000),
    -> (102,'sita',2,35000),
    -> (103,'keechu',1,45000);
Query OK, 3 rows affected (0.638 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|    101 | ravi     |             1 |  40000 |
|    102 | sita     |             2 |  35000 |
|    103 | keechu   |             1 |  45000 |
+--------+----------+---------------+--------+
3 rows in set (0.010 sec)

mysql> insert into employees values(104,'anu',5,30000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`intern_training_db`.`employees`, CONSTRAINT `employees_ibfk_1` FOREIGN KEY (`department_id`) REFERENCES `departments` (`department_id`))
mysql> drop table employees;
Query OK, 0 rows affected (0.669 sec)

mysql> create table employees(
    -> emp_id int primary key,
    -> emp_name varchar(50),
    -> department_id int,
    -> salary int,
    -> foreign key(department_id) references departments(department_id) on delete cascade
    -> );
Query OK, 0 rows affected (2.781 sec)

mysql> insert into employees values
    -> (101,'ravi',1,40000),
    -> (102,'sita',2,35000),
    -> (103,'keechu',1,45000);
Query OK, 3 rows affected (0.475 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> delete from departments where department_id=1;
Query OK, 1 row affected (0.485 sec)

mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|    102 | sita     |             2 |  35000 |
+--------+----------+---------------+--------+
1 row in set (0.009 sec)

mysql>










