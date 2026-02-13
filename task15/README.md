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

mysql> use company_db;
Database changed
mysql> describe employee;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| emp_id       | int         | NO   | PRI | NULL    |       |
| emp_name     | varchar(50) | YES  |     | NULL    |       |
| salary       | int         | YES  |     | NULL    |       |
| dept_name    | varchar(30) | YES  |     | NULL    |       |
| joining_date | date        | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.038 sec)

mysql> INSERT INTO employee VALUES
    -> (101,'Ravi',30000,'IT','2022-01-10'),
    -> (102,'Sita',35000,'IT','2021-03-15'),
    -> (103,'Kiran',28000,'HR','2023-02-20'),
    -> (104,'Anu',45000,'HR','2020-05-18'),
    -> (105,'John',40000,'IT','2022-07-11'),
    -> (106,'Meena',38000,'HR','2021-09-25');
ERROR 1062 (23000): Duplicate entry '101' for key 'employee.PRIMARY'
mysql> select*from employee;
+--------+----------+--------+-----------+--------------+
| emp_id | emp_name | salary | dept_name | joining_date |
+--------+----------+--------+-----------+--------------+
|    101 | ravi     |  30000 | NULL      | NULL         |
|    102 | sita     |  40000 | NULL      | NULL         |
|    103 | kiran    |  50000 | NULL      | NULL         |
|    104 | anu      |  45000 | NULL      | NULL         |
|    201 | Ravi     |  30000 | IT        | 2022-01-10   |
|    202 | Sita     |  35000 | IT        | 2021-03-15   |
|    203 | Kiran    |  28000 | HR        | 2023-02-20   |
|    204 | Anu      |  45000 | HR        | 2020-05-18   |
|    205 | John     |  40000 | IT        | 2022-07-11   |
|    206 | Meena    |  38000 | HR        | 2021-09-25   |
+--------+----------+--------+-----------+--------------+
10 rows in set (0.009 sec)

mysql> INSERT INTO employee VALUES
    -> (107,'Ravi',30000,'IT','2022-01-10'),
    -> (108,'Sita',35000,'IT','2021-03-15'),
    -> (109,'Kiran',28000,'HR','2023-02-20'),
    -> (110,'Anu',45000,'HR','2020-05-18'),
    -> (111,'John',40000,'IT','2022-07-11'),
    -> (112,'Meena',38000,'HR','2021-09-25');
Query OK, 6 rows affected (0.986 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> select*from employee;
+--------+----------+--------+-----------+--------------+
| emp_id | emp_name | salary | dept_name | joining_date |
+--------+----------+--------+-----------+--------------+
|    101 | ravi     |  30000 | NULL      | NULL         |
|    102 | sita     |  40000 | NULL      | NULL         |
|    103 | kiran    |  50000 | NULL      | NULL         |
|    104 | anu      |  45000 | NULL      | NULL         |
|    107 | Ravi     |  30000 | IT        | 2022-01-10   |
|    108 | Sita     |  35000 | IT        | 2021-03-15   |
|    109 | Kiran    |  28000 | HR        | 2023-02-20   |
|    110 | Anu      |  45000 | HR        | 2020-05-18   |
|    111 | John     |  40000 | IT        | 2022-07-11   |
|    112 | Meena    |  38000 | HR        | 2021-09-25   |
|    201 | Ravi     |  30000 | IT        | 2022-01-10   |
|    202 | Sita     |  35000 | IT        | 2021-03-15   |
|    203 | Kiran    |  28000 | HR        | 2023-02-20   |
|    204 | Anu      |  45000 | HR        | 2020-05-18   |
|    205 | John     |  40000 | IT        | 2022-07-11   |
|    206 | Meena    |  38000 | HR        | 2021-09-25   |
+--------+----------+--------+-----------+--------------+
16 rows in set (0.009 sec)

mysql> select emp_name,dept_name,salary,row_number()over(partition by dept_name order by salary desc)as row_num from employee;
+----------+-----------+--------+---------+
| emp_name | dept_name | salary | row_num |
+----------+-----------+--------+---------+
| kiran    | NULL      |  50000 |       1 |
| anu      | NULL      |  45000 |       2 |
| sita     | NULL      |  40000 |       3 |
| ravi     | NULL      |  30000 |       4 |
| Anu      | HR        |  45000 |       1 |
| Anu      | HR        |  45000 |       2 |
| Meena    | HR        |  38000 |       3 |
| Meena    | HR        |  38000 |       4 |
| Kiran    | HR        |  28000 |       5 |
| Kiran    | HR        |  28000 |       6 |
| John     | IT        |  40000 |       1 |
| John     | IT        |  40000 |       2 |
| Sita     | IT        |  35000 |       3 |
| Sita     | IT        |  35000 |       4 |
| Ravi     | IT        |  30000 |       5 |
| Ravi     | IT        |  30000 |       6 |
+----------+-----------+--------+---------+
16 rows in set (0.014 sec)

mysql> select emp_name,dept_name,salary,rank() over(partition by dept_name order by salary desc)as rank_no,dense_rank() over(partition by dept_name order by salary desc)as dense_rank_no from employee;
+----------+-----------+--------+---------+---------------+
| emp_name | dept_name | salary | rank_no | dense_rank_no |
+----------+-----------+--------+---------+---------------+
| kiran    | NULL      |  50000 |       1 |             1 |
| anu      | NULL      |  45000 |       2 |             2 |
| sita     | NULL      |  40000 |       3 |             3 |
| ravi     | NULL      |  30000 |       4 |             4 |
| Anu      | HR        |  45000 |       1 |             1 |
| Anu      | HR        |  45000 |       1 |             1 |
| Meena    | HR        |  38000 |       3 |             2 |
| Meena    | HR        |  38000 |       3 |             2 |
| Kiran    | HR        |  28000 |       5 |             3 |
| Kiran    | HR        |  28000 |       5 |             3 |
| John     | IT        |  40000 |       1 |             1 |
| John     | IT        |  40000 |       1 |             1 |
| Sita     | IT        |  35000 |       3 |             2 |
| Sita     | IT        |  35000 |       3 |             2 |
| Ravi     | IT        |  30000 |       5 |             3 |
| Ravi     | IT        |  30000 |       5 |             3 |
+----------+-----------+--------+---------+---------------+
16 rows in set (0.014 sec)

mysql> select emp_name,dept_name,salary,sum(salary)over(partition by dept_name order by salary)as running_total from employee;
+----------+-----------+--------+---------------+
| emp_name | dept_name | salary | running_total |
+----------+-----------+--------+---------------+
| ravi     | NULL      |  30000 |         30000 |
| sita     | NULL      |  40000 |         70000 |
| anu      | NULL      |  45000 |        115000 |
| kiran    | NULL      |  50000 |        165000 |
| Kiran    | HR        |  28000 |         56000 |
| Kiran    | HR        |  28000 |         56000 |
| Meena    | HR        |  38000 |        132000 |
| Meena    | HR        |  38000 |        132000 |
| Anu      | HR        |  45000 |        222000 |
| Anu      | HR        |  45000 |        222000 |
| Ravi     | IT        |  30000 |         60000 |
| Ravi     | IT        |  30000 |         60000 |
| Sita     | IT        |  35000 |        130000 |
| Sita     | IT        |  35000 |        130000 |
| John     | IT        |  40000 |        210000 |
| John     | IT        |  40000 |        210000 |
+----------+-----------+--------+---------------+
16 rows in set (0.017 sec)

mysql> select emp_name,salary,lag(salary)over(order by salary)as previous_salary,lead(salary)over(order by salary)as next_salary from employee;
+----------+--------+-----------------+-------------+
| emp_name | salary | previous_salary | next_salary |
+----------+--------+-----------------+-------------+
| Kiran    |  28000 |            NULL |       28000 |
| Kiran    |  28000 |           28000 |       30000 |
| ravi     |  30000 |           28000 |       30000 |
| Ravi     |  30000 |           30000 |       30000 |
| Ravi     |  30000 |           30000 |       35000 |
| Sita     |  35000 |           30000 |       35000 |
| Sita     |  35000 |           35000 |       38000 |
| Meena    |  38000 |           35000 |       38000 |
| Meena    |  38000 |           38000 |       40000 |
| sita     |  40000 |           38000 |       40000 |
| John     |  40000 |           40000 |       40000 |
| John     |  40000 |           40000 |       45000 |
| anu      |  45000 |           40000 |       45000 |
| Anu      |  45000 |           45000 |       45000 |
| Anu      |  45000 |           45000 |       50000 |
| kiran    |  50000 |           45000 |        NULL |
+----------+--------+-----------------+-------------+
16 rows in set (0.014 sec)

mysql> select dept_name,avg(salary) from employee group by dept_name;
+-----------+-------------+
| dept_name | avg(salary) |
+-----------+-------------+
| NULL      |  41250.0000 |
| IT        |  35000.0000 |
| HR        |  37000.0000 |
+-----------+-------------+
3 rows in set (0.220 sec)

mysql> select emp_name,dept_name,salary,avg(salary)over(partition by dept_name)as dept_avg from eemployee;
ERROR 1146 (42S02): Table 'company_db.eemployee' doesn't exist
mysql> select emp_name,dept_name,salary,avg(salary)over(partition by dept_name)as dept_avg from employee;
+----------+-----------+--------+------------+
| emp_name | dept_name | salary | dept_avg   |
+----------+-----------+--------+------------+
| ravi     | NULL      |  30000 | 41250.0000 |
| sita     | NULL      |  40000 | 41250.0000 |
| kiran    | NULL      |  50000 | 41250.0000 |
| anu      | NULL      |  45000 | 41250.0000 |
| Kiran    | HR        |  28000 | 37000.0000 |
| Anu      | HR        |  45000 | 37000.0000 |
| Meena    | HR        |  38000 | 37000.0000 |
| Kiran    | HR        |  28000 | 37000.0000 |
| Anu      | HR        |  45000 | 37000.0000 |
| Meena    | HR        |  38000 | 37000.0000 |
| Ravi     | IT        |  30000 | 35000.0000 |
| Sita     | IT        |  35000 | 35000.0000 |
| John     | IT        |  40000 | 35000.0000 |
| Ravi     | IT        |  30000 | 35000.0000 |
| Sita     | IT        |  35000 | 35000.0000 |
| John     | IT        |  40000 | 35000.0000 |
+----------+-----------+--------+------------+
16 rows in set (0.014 sec)

mysql> select*from(
    -> select emp_name,dept_name,salary,row_number()over(partition by dept_name order by salary desc)as rnk from employee
    -> )t
    -> where rnk=1;
+----------+-----------+--------+-----+
| emp_name | dept_name | salary | rnk |
+----------+-----------+--------+-----+
| kiran    | NULL      |  50000 |   1 |
| Anu      | HR        |  45000 |   1 |
| John     | IT        |  40000 |   1 |
+----------+-----------+--------+-----+
3 rows in set (0.409 sec)

mysql> select emp_nam,joining_date,salary,lag(salary)over(order by joining_date)as prev_salary from employee;
ERROR 1054 (42S22): Unknown column 'emp_nam' in 'field list'
mysql> select emp_name,joining_date,salary,lag(salary)over(order by joining_date)as prev_salary from employee;
+----------+--------------+--------+-------------+
| emp_name | joining_date | salary | prev_salary |
+----------+--------------+--------+-------------+
| ravi     | NULL         |  30000 |        NULL |
| sita     | NULL         |  40000 |       30000 |
| kiran    | NULL         |  50000 |       40000 |
| anu      | NULL         |  45000 |       50000 |
| Anu      | 2020-05-18   |  45000 |       45000 |
| Anu      | 2020-05-18   |  45000 |       45000 |
| Sita     | 2021-03-15   |  35000 |       45000 |
| Sita     | 2021-03-15   |  35000 |       35000 |
| Meena    | 2021-09-25   |  38000 |       35000 |
| Meena    | 2021-09-25   |  38000 |       38000 |
| Ravi     | 2022-01-10   |  30000 |       38000 |
| Ravi     | 2022-01-10   |  30000 |       30000 |
| John     | 2022-07-11   |  40000 |       30000 |
| John     | 2022-07-11   |  40000 |       40000 |
| Kiran    | 2023-02-20   |  28000 |       40000 |
| Kiran    | 2023-02-20   |  28000 |       28000 |
+----------+--------------+--------+-------------+
16 rows in set (0.015 sec)

mysql> select*from(
    -> select emp_name,dept_name,salary,dense_rank()over(partition by dept_name order by salary desc)as rnk from employee
    -> )t
    -> where rnk<=2;
+----------+-----------+--------+-----+
| emp_name | dept_name | salary | rnk |
+----------+-----------+--------+-----+
| kiran    | NULL      |  50000 |   1 |
| anu      | NULL      |  45000 |   2 |
| Anu      | HR        |  45000 |   1 |
| Anu      | HR        |  45000 |   1 |
| Meena    | HR        |  38000 |   2 |
| Meena    | HR        |  38000 |   2 |
| John     | IT        |  40000 |   1 |
| John     | IT        |  40000 |   1 |
| Sita     | IT        |  35000 |   2 |
| Sita     | IT        |  35000 |   2 |
+----------+-----------+--------+-----+
10 rows in set (0.014 sec)

mysql>











