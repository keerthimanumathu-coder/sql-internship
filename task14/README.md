Microsoft Windows [Version 10.0.26100.7623]
(c) Microsoft Corporation. All rights reserved.

C:\Users\KEERTHI>mysql --version
mysql  Ver 9.5.0 for Win64 on x86_64 (MySQL Community Server - GPL)

C:\Users\KEERTHI>mysql -u root -p
Enter password: **********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 19
Server version: 9.5.0 MySQL Community Server - GPL

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use intern_training_db;
Database changed
mysql> create database  company_db;
Query OK, 1 row affected (0.242 sec)

mysql> use company_db;
Database changed
mysql> create table employee(
    -> emp_id int primary key,
    -> emp_name varchar(50),
    -> salary int
    -> )ENGINE=innodb;
Query OK, 0 rows affected (0.353 sec)

mysql> DELIMITER //
mysql>
mysql> CREATE PROCEDURE add_employee(
    ->     IN p_id INT,
    ->     IN p_name VARCHAR(50),
    ->     IN p_salary INT
    -> )
    -> BEGIN
    ->     INSERT INTO employee VALUES (p_id, p_name, p_salary);
    -> END //
Query OK, 0 rows affected (0.406 sec)

mysql>
mysql> DELIMITER ;
mysql> call add_employee(101,'ravi',30000);
Query OK, 1 row affected (0.486 sec)

mysql> call add_employee(102,'sita',40000);
Query OK, 1 row affected (0.482 sec)

mysql> select*from employee;
+--------+----------+--------+
| emp_id | emp_name | salary |
+--------+----------+--------+
|    101 | ravi     |  30000 |
|    102 | sita     |  40000 |
+--------+----------+--------+
2 rows in set (0.391 sec)

mysql> DELIMITER //
mysql>
mysql> CREATE FUNCTION calculate_tax(sal INT)
    -> RETURNS INT
    -> DETERMINISTIC
    -> BEGIN
    ->     RETURN sal * 10 / 100;
    -> END //
Query OK, 0 rows affected (0.289 sec)

mysql>
mysql> DELIMITER ;
mysql> select emp_name,salary,calculate_tax(salary)as tax from employee;
+----------+--------+------+
| emp_name | salary | tax  |
+----------+--------+------+
| ravi     |  30000 | 3000 |
| sita     |  40000 | 4000 |
+----------+--------+------+
2 rows in set (0.021 sec)

mysql> DELIMITER //
mysql>
mysql> CREATE PROCEDURE safe_add_employee(
    ->     IN p_id INT,
    ->     IN p_name VARCHAR(50),
    ->     IN p_salary INT
    -> )
    -> BEGIN
    ->     DECLARE EXIT HANDLER FOR SQLEXCEPTION
    ->     BEGIN
    ->         SELECT 'Error occurred' AS Message;
    ->     END;
    ->
    ->     INSERT INTO employee VALUES (p_id, p_name, p_salary);
    ->     SELECT 'Inserted Successfully' AS Message;
    -> END //
Query OK, 0 rows affected (0.934 sec)

mysql>
mysql> DELIMITER ;
mysql> call safe_add_employee(101,'ram',25000);
+----------------+
| Message        |
+----------------+
| Error occurred |
+----------------+
1 row in set (0.390 sec)

Query OK, 0 rows affected (0.409 sec)

mysql> call add_employee(103,'kiran',50000);
Query OK, 1 row affected (0.468 sec)

mysql> call add_employee(104,'anu',45000);
Query OK, 1 row affected (0.549 sec)

mysql>
