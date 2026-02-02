Microsoft Windows [Version 10.0.26100.7623]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> select*from employees where emp_name='ravi';
Empty set (0.015 sec)

mysql> show index from employees;
+-----------+------------+---------------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table     | Non_unique | Key_name      | Seq_in_index | Column_name   | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-----------+------------+---------------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| employees |          0 | PRIMARY       |            1 | emp_id        | A         |           3 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| employees |          1 | department_id |            1 | department_id | A         |           1 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+-----------+------------+---------------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
2 rows in set (0.041 sec)

mysql> select*from employees where emp_name='ravi';
Empty set (0.010 sec)

mysql> create index idx_emp_name on employees(emp_name);
Query OK, 0 rows affected (1.002 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select*from employees where emp_name='ravi';
Empty set (0.013 sec)

mysql> explain select*from employees where emp_name='ravi';
+------------------------------------------------------------------------------------------+
| EXPLAIN                                                                                  |
+------------------------------------------------------------------------------------------+
| -> Index lookup on employees using idx_emp_name (emp_name = 'ravi')  (cost=0.35 rows=1)
 |
+------------------------------------------------------------------------------------------+
1 row in set (0.013 sec)

mysql> explain select*from employees where emp_name='ravi';
+------------------------------------------------------------------------------------------+
| EXPLAIN                                                                                  |
+------------------------------------------------------------------------------------------+
| -> Index lookup on employees using idx_emp_name (emp_name = 'ravi')  (cost=0.35 rows=1)
 |
+------------------------------------------------------------------------------------------+
1 row in set (0.012 sec)

mysql> create table employees(
    -> emp_id int primary key,
    -> emp_name varchar(50),
    -> dept_id int
    -> );
ERROR 1050 (42S01): Table 'employees' already exists
mysql> desc employees;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| emp_id        | int         | NO   | PRI | NULL    |       |
| emp_name      | varchar(50) | YES  | MUL | NULL    |       |
| department_id | int         | YES  | MUL | NULL    |       |
| salary        | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.176 sec)

mysql> insert into employees values(20,'test',1);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|      7 | anu      |             2 |   NULL |
|      8 | ramesh   |             2 |   NULL |
|    102 | sita     |             2 |  45000 |
+--------+----------+---------------+--------+
3 rows in set (0.010 sec)

mysql> insert into employees values(20,'keechu',20000);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> insert into employees values(20,'keechu',1,20000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`intern_training_db`.`employees`, CONSTRAINT `employees_ibfk_1` FOREIGN KEY (`department_id`) REFERENCES `departments` (`department_id`) ON DELETE CASCADE)
mysql> DESC employees;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| emp_id        | int         | NO   | PRI | NULL    |       |
| emp_name      | varchar(50) | YES  | MUL | NULL    |       |
| department_id | int         | YES  | MUL | NULL    |       |
| salary        | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.033 sec)

mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|      7 | anu      |             2 |   NULL |
|      8 | ramesh   |             2 |   NULL |
|    102 | sita     |             2 |  45000 |
+--------+----------+---------------+--------+
3 rows in set (0.010 sec)

mysql> UPDATE employees
    -> SET salary=30000
    -> WHERE emp_id=7;
Query OK, 1 row affected (0.250 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE employees
    -> SET salary=320000
    -> WHERE emp_id=8;
Query OK, 1 row affected (0.066 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|      7 | anu      |             2 |  30000 |
|      8 | ramesh   |             2 | 320000 |
|    102 | sita     |             2 |  45000 |
+--------+----------+---------------+--------+
3 rows in set (0.010 sec)

mysql>
