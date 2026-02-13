CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    department VARCHAR(50),
    salary INT,
    joining_date DATE
);
INSERT INTO employees VALUES
(1, 'Asha', 'HR', 30000, '2022-01-10'),
(2, 'Ravi', 'IT', 50000, '2021-03-15'),
(3, 'Meena', 'IT', 60000, '2020-07-20'),
(4, 'Kiran', 'HR', 35000, '2023-02-01'),
(5, 'Arjun', 'Sales', 40000, '2021-11-25'),
(6, 'Divya', 'Sales', 45000, '2022-05-30');
SELECT * FROM employees;
SELECT *,
ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_num
FROM employees;
SELECT emp_name, department, salary,
RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_no,
DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dense_rank_no
FROM employees;
SELECT emp_name, department, salary,
SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS running_total
FROM employees;
SELECT emp_name, department, salary,
AVG(salary) OVER (PARTITION BY department) AS dept_avg_salary
FROM employees;
SELECT *
FROM (
    SELECT emp_name, department, salary,
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank_no
    FROM employees
) t
WHERE rank_no = 1;
SELECT emp_name, joining_date, salary,
SUM(salary) OVER (ORDER BY joining_date) AS company_growth_salary
FROM employees;
