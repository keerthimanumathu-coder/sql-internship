Microsoft Windows [Version 10.0.26100.7623]
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
mysql> select e.emp_id,e.emp_name,d.department_name from employees e join departments d on e.department_id=d.department_id;
+--------+----------+-----------------+
| emp_id | emp_name | department_name |
+--------+----------+-----------------+
|      7 | anu      | HR              |
|    102 | sita     | HR              |
+--------+----------+-----------------+
2 rows in set (0.014 sec)

mysql> create view emp_view as select emp_id,emp_name,department_id from employees;
Query OK, 0 rows affected (0.550 sec)

mysql> insert into emp_view values(8,'ramesh',1);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`intern_training_db`.`employees`, CONSTRAINT `employees_ibfk_1` FOREIGN KEY (`department_id`) REFERENCES `departments` (`department_id`) ON DELETE CASCADE)
mysql> insert into emp_view values(8,'ramesh',2);
Query OK, 1 row affected (0.623 sec)

mysql> select*from emp_view;
+--------+----------+---------------+
| emp_id | emp_name | department_id |
+--------+----------+---------------+
|      7 | anu      |             2 |
|      8 | ramesh   |             2 |
|    102 | sita     |             2 |
+--------+----------+---------------+
3 rows in set (0.010 sec)

mysql> select*from emp_view where department_name='CSE';
ERROR 1054 (42S22): Unknown column 'department_name' in 'where clause'
mysql> select*from emp_view where department_id=2;
+--------+----------+---------------+
| emp_id | emp_name | department_id |
+--------+----------+---------------+
|      7 | anu      |             2 |
|      8 | ramesh   |             2 |
|    102 | sita     |             2 |
+--------+----------+---------------+
3 rows in set (0.412 sec)

mysql> select*from emp_view order by emp_name asc;
+--------+----------+---------------+
| emp_id | emp_name | department_id |
+--------+----------+---------------+
|      7 | anu      |             2 |
|      8 | ramesh   |             2 |
|    102 | sita     |             2 |
+--------+----------+---------------+
3 rows in set (0.011 sec)

mysql> insert into emp_view values(103,'keechu','CSE');
ERROR 1366 (HY000): Incorrect integer value: 'CSE' for column 'department_id' at row 1
mysql> drop view emp_view;
Query OK, 0 rows affected (0.487 sec)

mysql> create view emp_view as select e.emp_id,e.emp_name,d.department_name from employees e join departments d on e.department_id=d.department_id;
Query OK, 0 rows affected (0.688 sec)

mysql> select department_name,count(emp_id) from emp_view group by department_name;
+-----------------+---------------+
| department_name | count(emp_id) |
+-----------------+---------------+
| HR              |             3 |
+-----------------+---------------+
1 row in set (0.078 sec)

mysql>
