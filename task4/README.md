Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 45
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> select*from students order by name ASC;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.462 sec)

mysql> select*from students order by dob desc;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.016 sec)

mysql> select*from students order by current_city asc,name asc;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.013 sec)

mysql> select*from students order by age desc,name asc;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.013 sec)

mysql> select*from students limit 2;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.011 sec)

mysql> select*from students limit 1;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.011 sec)

mysql> select*from students where current_city='hyderabad' order by name asc;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
1 row in set (0.488 sec)

mysql> select*from students where age>18 order by dob;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.013 sec)

mysql> select*from students limit 2 offset 0;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
+----+--------+------------+------------------+--------------+------+
2 rows in set (0.012 sec)

mysql> select*from students limit 2 offset 2;
+----+------+------------+----------------+--------------+------+
| id | name | dob        | email          | current_city | age  |
+----+------+------------+----------------+--------------+------+
|  3 | sita | 2006-05-20 | sita@gmail.com | NULL         |   18 |
+----+------+------------+----------------+--------------+------+
1 row in set (0.012 sec)

mysql> select*from students order by id limit 5;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.011 sec)

mysql> select name,age from students order by age asc;
+--------+------+
| name   | age  |
+--------+------+
| sita   |   18 |
| keechu |   20 |
| ravi   |   22 |
+--------+------+
3 rows in set (0.012 sec)

mysql> select name,age from students order by age asc limit3;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'limit3' at line 1
mysql> select name,age from students order by age asc limit 3;
+--------+------+
| name   | age  |
+--------+------+
| sita   |   18 |
| keechu |   20 |
| ravi   |   22 |
+--------+------+
3 rows in set (0.012 sec)

mysql> select*from students order by current_city is null,current_city;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.418 sec)

mysql> select*from students order by name;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.010 sec)

mysql> select*from students limit 10;
+----+--------+------------+------------------+--------------+------+
| id | name   | dob        | email            | current_city | age  |
+----+--------+------------+------------------+--------------+------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |   20 |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |   22 |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |   18 |
+----+--------+------------+------------------+--------------+------+
3 rows in set (0.010 sec)

mysql>










