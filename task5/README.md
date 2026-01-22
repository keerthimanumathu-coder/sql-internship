Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 46
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> select count(*)from students;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.582 sec)

mysql> select count(age) as total_students,sum(age) as total_age,avg(age) as average_age,min(age) as min_age,max(age) as max_age from students;
+----------------+-----------+-------------+---------+---------+
| total_students | total_age | average_age | min_age | max_age |
+----------------+-----------+-------------+---------+---------+
|              3 |        60 |     20.0000 |      18 |      22 |
+----------------+-----------+-------------+---------+---------+
1 row in set (0.589 sec)

mysql> select age,count(*) as student_count from students group by age;
+------+---------------+
| age  | student_count |
+------+---------------+
|   20 |             1 |
|   22 |             1 |
|   18 |             1 |
+------+---------------+
3 rows in set (0.548 sec)

mysql> select age,count(*) as count_students from students group by age;
+------+----------------+
| age  | count_students |
+------+----------------+
|   20 |              1 |
|   22 |              1 |
|   18 |              1 |
+------+----------------+
3 rows in set (0.012 sec)

mysql> select current_city,count(*) as total_students from students group by current_city;
+--------------+----------------+
| current_city | total_students |
+--------------+----------------+
| hyderabad    |              1 |
| NULL         |              2 |
+--------------+----------------+
2 rows in set (0.400 sec)

mysql> select age,count(*) as student_count from students group by age having count(*)>1;
Empty set (0.061 sec)

mysql> select current_city,count(*) from students group by current_city having count(*)>=1;
+--------------+----------+
| current_city | count(*) |
+--------------+----------+
| hyderabad    |        1 |
| NULL         |        2 |
+--------------+----------+
2 rows in set (0.014 sec)

mysql> select*from students where age>18;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.010 sec)

mysql> select age,count(*) from students group by age having count(*)>1;
Empty set (0.013 sec)

mysql> select current_city as department,count(*) as total_students from students group by current_city;
+------------+----------------+
| department | total_students |
+------------+----------------+
| hyderabad  |              1 |
| NULL       |              2 |
+------------+----------------+
2 rows in set (0.012 sec)

mysql> select age,count(*) as student_count from students group by age;
+------+---------------+
| age  | student_count |
+------+---------------+
|   20 |             1 |
|   22 |             1 |
|   18 |             1 |
+------+---------------+
3 rows in set (0.012 sec)

mysql> select count(current_city) from students;
+---------------------+
| count(current_city) |
+---------------------+
|                   1 |
+---------------------+
1 row in set (0.011 sec)

mysql> select count(*) from students;
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.010 sec)

mysql> select current_city,count(*) from students group by current_city;
+--------------+----------+
| current_city | count(*) |
+--------------+----------+
| hyderabad    |        1 |
| NULL         |        2 |
+--------------+----------+
2 rows in set (0.011 sec)

mysql>









