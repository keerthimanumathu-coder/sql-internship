Microsoft Windows [Version 10.0.26100.7462]
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
mysql> select*from employees;
+--------+----------+---------------+--------+
| emp_id | emp_name | department_id | salary |
+--------+----------+---------------+--------+
|    102 | sita     |             2 |  35000 |
+--------+----------+---------------+--------+
1 row in set (0.011 sec)

mysql> select*from departments;
+---------------+-----------------+
| department_id | department_name |
+---------------+-----------------+
|             2 | HR              |
|             3 | Finance         |
+---------------+-----------------+
2 rows in set (0.012 sec)

mysql> select e.emp_id,e.emp_name,d.department_name from employees e inner join departments d on e.department_id=d.department_id;
+--------+----------+-----------------+
| emp_id | emp_name | department_name |
+--------+----------+-----------------+
|    102 | sita     | HR              |
+--------+----------+-----------------+
1 row in set (0.013 sec)

mysql> select e.emp_id,e.emp_name.d.department_name from employees e left join departments d on e.department_id=d.department_id;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.department_name from employees e left join departments d on e.department_id=d.d' at line 1
mysql> select e.emp_id,e.emp_name,d.department_name from employees e left join departments d on e.department_id=d.department_id;
+--------+----------+-----------------+
| emp_id | emp_name | department_name |
+--------+----------+-----------------+
|    102 | sita     | HR              |
+--------+----------+-----------------+
1 row in set (0.382 sec)

mysql> select e.emp_name,d.department_name from employees e right join departments d on e.department_id=d.department_id;
+----------+-----------------+
| emp_name | department_name |
+----------+-----------------+
| sita     | HR              |
| NULL     | Finance         |
+----------+-----------------+
2 rows in set (0.435 sec)

mysql> select e.emp_name,d.department_name from employees e left join departments d on e.department_id=d.department_id union select e.emp_name,d.department_name from employees e right join departments d on e.department_id=d.department_id;
+----------+-----------------+
| emp_name | department_name |
+----------+-----------------+
| sita     | HR              |
| NULL     | Finance         |
+----------+-----------------+
2 rows in set (0.440 sec)

mysql> select e.emp_name,d.department_name from employees as e join departments as d on e.department_id=d.department_id;
+----------+-----------------+
| emp_name | department_name |
+----------+-----------------+
| sita     | HR              |
+----------+-----------------+
1 row in set (0.011 sec)

mysql>












