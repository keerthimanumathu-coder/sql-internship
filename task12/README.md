Microsoft Windows [Version 10.0.26100.7623]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 15
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> CREATE TABLE employee (
    ->     emp_id INT PRIMARY KEY,
    ->     emp_name VARCHAR(50) UNIQUE,
    ->     age INT CHECK (age BETWEEN 18 AND 60),
    ->     salary INT CHECK (salary >= 10000),
    ->     dept VARCHAR(20),
    ->     created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    -> );
Query OK, 0 rows affected (1.895 sec)

mysql> insert into employee values(1,'rama',25,20000,'cse',default);
Query OK, 1 row affected (0.508 sec)

mysql> insert into employee values(2,'priya',15,15000,'ece',default);
ERROR 3819 (HY000): Check constraint 'employee_chk_1' is violated.
mysql> insert into employee(emp_id,emp_name,age,salary,dept)
    -> values(3,'arjun',30,25000,'cse');
Query OK, 1 row affected (0.239 sec)

mysql> select emp_id,created_at from employee;
+--------+---------------------+
| emp_id | created_at          |
+--------+---------------------+
|      1 | 2026-02-10 20:01:11 |
|      3 | 2026-02-10 20:03:43 |
+--------+---------------------+
2 rows in set (0.113 sec)

mysql> insert into employee values(4,'keechu',28,22000,'eee',default);
Query OK, 1 row affected (0.449 sec)

mysql> create table student(
    -> roll_no int primary key,
    -> marks int check(marks between 0 and 100) default 40
    -> );
Query OK, 0 rows affected (0.714 sec)

mysql> insert into student(roll_no)values(1);
Query OK, 1 row affected (0.105 sec)

mysql> show create table employee;
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table    | Create Table                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| employee | CREATE TABLE `employee` (
  `emp_id` int NOT NULL,
  `emp_name` varchar(50) DEFAULT NULL,
  `age` int DEFAULT NULL,
  `salary` int DEFAULT NULL,
  `dept` varchar(20) DEFAULT NULL,
  `created_at` timestamp NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`emp_id`),
  UNIQUE KEY `emp_name` (`emp_name`),
  CONSTRAINT `employee_chk_1` CHECK ((`age` between 18 and 60)),
  CONSTRAINT `employee_chk_2` CHECK ((`salary` >= 10000))
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
+----------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.466 sec)

mysql> desc employee;
+------------+-------------+------+-----+-------------------+-------------------+
| Field      | Type        | Null | Key | Default           | Extra             |
+------------+-------------+------+-----+-------------------+-------------------+
| emp_id     | int         | NO   | PRI | NULL              |                   |
| emp_name   | varchar(50) | YES  | UNI | NULL              |                   |
| age        | int         | YES  |     | NULL              |                   |
| salary     | int         | YES  |     | NULL              |                   |
| dept       | varchar(20) | YES  |     | NULL              |                   |
| created_at | timestamp   | YES  |     | CURRENT_TIMESTAMP | DEFAULT_GENERATED |
+------------+-------------+------+-----+-------------------+-------------------+
6 rows in set (0.590 sec)

mysql>












