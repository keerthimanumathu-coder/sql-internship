Microsoft Windows [Version 10.0.26100.7623]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 18
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> CREATE TABLE accounts (
    ->     acc_no INT PRIMARY KEY,
    ->     name VARCHAR(50),
    ->     balance INT
    -> ) ENGINE=InnoDB;
Query OK, 0 rows affected (0.342 sec)

mysql> insert into accounts values
    -> (101,'ravi',10000),
    -> (102,'sita',8000);
Query OK, 2 rows affected (0.492 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.007 sec)

mysql>
mysql> UPDATE accounts SET balance = balance - 1000 WHERE acc_no = 101;
Query OK, 1 row affected (0.391 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE accounts SET balance = balance + 1000 WHERE acc_no = 102;
Query OK, 1 row affected (0.008 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql>
mysql> COMMIT;
Query OK, 0 rows affected (0.493 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.005 sec)

mysql> commit;
Query OK, 0 rows affected (0.006 sec)

mysql> start transaction;
Query OK, 0 rows affected (0.006 sec)

mysql> update accounts set balance=balance-5000 where acc_no=101;
Query OK, 1 row affected (0.012 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> rollback;
Query OK, 0 rows affected (0.422 sec)

mysql> set transaction isolation level serializable;
Query OK, 0 rows affected (0.887 sec)

mysql> set transaction isolation level read committed;
Query OK, 0 rows affected (0.006 sec)

mysql>
