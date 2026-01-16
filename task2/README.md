Microsoft Windows [Version 10.0.26100.7462]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 41
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>  use intern_training_db;
Database changed
mysql> drop table if exists students;
Query OK, 0 rows affected (0.717 sec)

mysql> create table students(
    -> id INT PRIMARY KEY,
    -> name VARCHAR(50)NOT NULL,
    -> age INT,
    -> dob DATE,
    -> email VARCHAR(100)UNIQUE
    -> );
Query OK, 0 rows affected (0.892 sec)

mysql> insert into students values(1,'keechu',20,'2005-02-10','keechu@gmail.com');
Query OK, 1 row affected (0.437 sec)

mysql> insert into students values(2,'ravi',21,'2004-08-15','ravi@gmail.com');
Query OK, 1 row affected (0.754 sec)

mysql> insert into students values(3,'sita',19,'2006-05-20','sita@gmail.com');
Query OK, 1 row affected (0.440 sec)

mysql> select*from students;
+----+--------+------+------------+------------------+
| id | name   | age  | dob        | email            |
+----+--------+------+------------+------------------+
|  1 | keechu |   20 | 2005-02-10 | keechu@gmail.com |
|  2 | ravi   |   21 | 2004-08-15 | ravi@gmail.com   |
|  3 | sita   |   19 | 2006-05-20 | sita@gmail.com   |
+----+--------+------+------------+------------------+
3 rows in set (0.011 sec)

mysql> insert into students values(1,'ravi','ravi@gmail.com',21);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> insert into students values(2,NULL,'sita@gmail.com',19);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> insert into students values(3,'anu','keechu@gmail.com',20);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> select*from students;
+----+--------+------+------------+------------------+
| id | name   | age  | dob        | email            |
+----+--------+------+------------+------------------+
|  1 | keechu |   20 | 2005-02-10 | keechu@gmail.com |
|  2 | ravi   |   21 | 2004-08-15 | ravi@gmail.com   |
|  3 | sita   |   19 | 2006-05-20 | sita@gmail.com   |
+----+--------+------+------------+------------------+
3 rows in set (0.009 sec)

mysql> ALTER TABLE students ADD COLUMN city VARCHAR(50);
Query OK, 0 rows affected (0.437 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE students;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int          | NO   | PRI | NULL    |       |
| name  | varchar(50)  | NO   |     | NULL    |       |
| age   | int          | YES  |     | NULL    |       |
| dob   | date         | YES  |     | NULL    |       |
| email | varchar(100) | YES  | UNI | NULL    |       |
| city  | varchar(50)  | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
6 rows in set (0.035 sec)

mysql> UPDATE students SET city='hyderabad' WHERE id=1;
Query OK, 1 row affected (0.499 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> ALTER TABLE students CHANGE COLUMN city current_city VARCHAR(50);
Query OK, 0 rows affected (0.666 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE students;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| id           | int          | NO   | PRI | NULL    |       |
| name         | varchar(50)  | NO   |     | NULL    |       |
| age          | int          | YES  |     | NULL    |       |
| dob          | date         | YES  |     | NULL    |       |
| email        | varchar(100) | YES  | UNI | NULL    |       |
| current_city | varchar(50)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
6 rows in set (0.028 sec)

mysql> ALTER TABLE students DROP COLUMN age;
Query OK, 0 rows affected (0.757 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE students;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| id           | int          | NO   | PRI | NULL    |       |
| name         | varchar(50)  | NO   |     | NULL    |       |
| dob          | date         | YES  |     | NULL    |       |
| email        | varchar(100) | YES  | UNI | NULL    |       |
| current_city | varchar(50)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
5 rows in set (0.029 sec)

mysql> select*from students;
+----+--------+------------+------------------+--------------+
| id | name   | dob        | email            | current_city |
+----+--------+------------+------------------+--------------+
|  1 | keechu | 2005-02-10 | keechu@gmail.com | hyderabad    |
|  2 | ravi   | 2004-08-15 | ravi@gmail.com   | NULL         |
|  3 | sita   | 2006-05-20 | sita@gmail.com   | NULL         |
+----+--------+------------+------------------+--------------+
3 rows in set (0.010 sec)

mysql> DESCRIBE students;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| id           | int          | NO   | PRI | NULL    |       |
| name         | varchar(50)  | NO   |     | NULL    |       |
| dob          | date         | YES  |     | NULL    |       |
| email        | varchar(100) | YES  | UNI | NULL    |       |
| current_city | varchar(50)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
5 rows in set (0.030 sec)

mysql>










