Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 44
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> select*from students;
+----+--------+------------+------------------+--------------+
| id | name   | dob        | email            | current_city |
+----+--------+------------+------------------+--------------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |
+----+--------+------------+------------------+--------------+
3 rows in set (0.015 sec)

mysql> alter table students add age INT;
Query OK, 0 rows affected (0.709 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc students;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| id           | int          | NO   | PRI | NULL    |       |
| name         | varchar(50)  | NO   |     | NULL    |       |
| dob          | date         | YES  |     | NULL    |       |
| email        | varchar(100) | YES  | UNI | NULL    |       |
| current_city | varchar(50)  | YES  |     | NULL    |       |
| age          | int          | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
6 rows in set (0.424 sec)

mysql> update students set age=20 where id=1;
Query OK, 1 row affected (0.452 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update students set age=22 where id=2;
Query OK, 1 row affected (0.130 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update students set age=18 where id=3;
Query OK, 1 row affected (0.678 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select*from students;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.010 sec)

mysql> select*from students where age=20;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.012 sec)

mysql> select*from students where age>18;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.024 sec)

mysql> select*from students where age>18 and city='hyderabad';
ERROR 1054 (42S22): Unknown column 'city' in 'where clause'
mysql> select*from students where age>18 and current_city='hyderabad';
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.011 sec)

mysql> select*from students where current_city='hyderabad' or email is not null;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.389 sec)

mysql> select *from students where name  like'A%';
Empty set (0.440 sec)

mysql> select*from students where name like'%i';
+----+------+------------+----------------+--------------+------+
| id | name | dob        | email          | current_city | age  |
+----+------+------------+----------------+--------------+------+
|  2 | ravi | 2004-08-15 | ravi@gmail.com | NULL         |   22 |
+----+------+------------+----------------+--------------+------+
1 row in set (0.011 sec)

mysql> select*from students where name like'_e%';
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.010 sec)

mysql> select*from students where name in('keechu','sita');
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.010 sec)

mysql> select*from students where current_city in('hyderabad','chennai');
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.011 sec)

mysql> select*from students where age between 18 and 22;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.044 sec)

mysql> select*from students where email is null;
Empty set (0.014 sec)

mysql> select*from students where email is not null;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.011 sec)

mysql> select name,age from students where age>20;
+------+------+
| name | age  |
+------+------+
| ravi |   22 |
+------+------+
1 row in set (0.013 sec)

mysql> select name as student_name,age as student_age from students;
+--------------+-------------+
| student_name | student_age |
+--------------+-------------+
| keechu       |          20 |
| ravi         |          22 |
| sita         |          18 |
+--------------+-------------+
3 rows in set (0.010 sec)

mysql> select s.name,s.city from students s where s.age>18;
ERROR 1054 (42S22): Unknown column 's.city' in 'field list'
mysql> select s.name,s.current_city from students s where s.age>18;
+--------+--------------+
| name   | current_city |
+--------+--------------+
| keechu | hyderabad    |
| ravi   | NULL         |
+--------+--------------+
2 rows in set (0.010 sec)

mysql> select*from students where email like'%gmail.com';
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.011 sec)

mysql> select*from students where email='ravi@gmail.com';
+----+------+------------+----------------+--------------+------+
| id | name | dob        | email          | current_city | age  |
+----+------+------------+----------------+--------------+------+
|  2 | ravi | 2004-08-15 | ravi@gmail.com | NULL         |   22 |
+----+------+------------+----------------+--------------+------+
1 row in set (0.012 sec)

mysql> select*from students where email like '%@college.edu';
Empty set (0.011 sec)

mysql>










