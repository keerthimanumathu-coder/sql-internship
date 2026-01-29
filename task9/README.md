Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 16
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> desc employees;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| emp_id        | int         | NO   | PRI | NULL    |       |
| emp_name      | varchar(50) | YES  |     | NULL    |       |
| department_id | int         | YES  | MUL | NULL    |       |
| salary        | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.043 sec)

mysql> update employees set salary=30000 where emp_id=101;
Query OK, 0 rows affected (0.419 sec)
Rows matched: 0  Changed: 0  Warnings: 0

mysql> update employees set salary=45000 where emp_id=102;
Query OK, 1 row affected (0.476 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update employees set salary=25000 where emp_id=103;
Query OK, 0 rows affected (0.011 sec)
Rows matched: 0  Changed: 0  Warnings: 0

mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|    102 | sita     |             2 |  45000 |
+--------+----------+---------------+--------+
1 row in set (0.009 sec)

mysql> select emp_name,salary from employees where salary>(select avg(salary)from employees);
Empty set (0.482 sec)

mysql> select emp_name from employees where department_id=(select department_id from departments where department_name='HR');
+----------+
| emp_name |
+----------+
| sita     |
+----------+
1 row in set (0.015 sec)

mysql> select avg_sal.avg_salary from(select avg(salary)as avg_salary from employees)avg_sal;
+------------+
| avg_salary |
+------------+
| 45000.0000 |
+------------+
1 row in set (0.012 sec)

mysql> select emp_name,salary,(select avg(salary)from employees) as avg_salary from employees;
+----------+--------+------------+
| emp_name | salary | avg_salary |
+----------+--------+------------+
| sita     |  45000 | 45000.0000 |
+----------+--------+------------+
1 row in set (0.012 sec)

mysql> select emp_name from employees where department_id=(select department_id from departments where department_name='HR');
+----------+
| emp_name |
+----------+
| sita     |
+----------+
1 row in set (0.011 sec)

mysql> select e.emp_name from employees e join departments d on e.department_id=d.department_id where d.department_name='HR';
+----------+
| emp_name |
+----------+
| sita     |
+----------+
1 row in set (0.012 sec)

mysql> select emp_name,salary from employees e where salary>(select avg(salary)from employees where department_id=e.department_id);
Empty set (0.013 sec)

mysql> select emp_name from employees e where exists(select 1 from departments d where d.department_id=e.department_id);
+----------+
| emp_name |
+----------+
| sita     |
+----------+
1 row in set (0.033 sec)

mysql> select emp_name from employees where department_id in(select department_id from departments);
+----------+
| emp_name |
+----------+
| sita     |
+----------+
1 row in set (0.011 sec)

mysql>
