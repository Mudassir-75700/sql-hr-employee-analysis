# sql-hr-employee-analysis
This project demonstrates SQL skills by analyzing an HR employee dataset using MySQL. The project covers database creation, data cleaning, data transformation, and business-focused analysis through SQL queries.
HR Employee Data Analysis using SQL
Project Overview

This project demonstrates SQL skills by analyzing an HR employee dataset using MySQL. The project covers database creation, data cleaning, data transformation, and business-focused analysis through SQL queries.

Objectives
Create and manage an HR database
Clean and prepare employee data
Perform exploratory data analysis
Answer business questions using SQL
Practice advanced SQL concepts such as CTEs and Window Functions
Database Operations
Created MySQL database
Renamed tables and columns
Modified data types
Updated missing salary values
Cleaned inconsistent data
SQL Concepts Used
create database HR_Data;
use hr_data;
select * from hr data;

alter table hr data
rename to hr_employees;

select * from hr_employees;

alter table hr_employees
modify column join_date DATE;

ALTER TABLE hr_employees
RENAME COLUMN joining_date TO hire_date;

ALTER TABLE hr_employees
MODIFY COLUMN salary_INR DECIMAL(10,2);

select employee_id,salary_inr from hr_employees
where salary_inr is NULL;

UPDATE hr_employees
set salary_inr = 50000
where EMPLOYEE_ID='EMP0001';

set SQL_safe_updates=0;

describe hr_employees;

select salary_inr from hr_employees 
where salary_inr ='';

UPDATE hr_employees
SET salary_inr = 45000
where salary_inr=0;

ALTER TABLE hr_employees
MODIFY COLUMN salary_INR DECIMAL(10,2);

ALTER TABLE hr_employees
MODIFY COLUMN AGE INT;

ALTER TABLE hr_employees
RENAME COLUMN emp_id TO Emp_id;



use hr_data;


-- TOTAL EMPLOYEES

select count(emp_id) total_emp 
from employees;

-- How many Departments are there in the Data?

select distinct(department) Department 
from employees;

-- How many Male and Female Count in Data

select gender,count(*) Gender_Count 
from employees
GROUP BY gender;

-- Employees City Wise

select DISTINCT(city) Employees_City 
from employees
ORDER BY Employees_City ASC;

-- How many Employees in Each department?

select Department,count(emp_id) Total_Emp
FROM employees 
Group by Department
ORDER BY DEpartment ASC;


												-- LEVEL 2: Intermediate Analysis (6–12)

-- What is the average salary in each department?

select department,
ROUND(avg(salary),2) avg_salary 
FROM employees
GROUP BY department
ORDER BY department ASC;

-- Which employee has the highest salary?

select Name,salary
FROM employees
WHERE salary = 
(select max(salary) from employees);
													 -- OR --
select Name,salary
FROM employees
ORDER BY salary DESC
LIMIT 1;

-- Which employee has the lowest salary?

select Name,salary as min_salary
FROM employees
WHERE salary = 
(select MIN(salary) from employees);

-- Who are the top 5 highest-paid employees?

select Name,salary as Max_salary
FROM employees
ORDER BY salary DESC
LIMIT 5;

-- What is the average salary based on years of experience?

select years_at_company,
COUNT(*) Emp_Count,
ROUND(AVG(salary),2) avg_sal
FROM employees
GROUP BY years_at_company
ORDER BY years_at_company;

-- How many employees are there in each city?

select City,
Count(emp_id)
employees_count
FROM employees
GROUP BY city
ORDER BY employees_count DESC;

-- How many employees are there in each job role?

select job_title,
COUNT(*) emp_count
FROM employees
GROUP BY job_title
ORDER BY emp_count DESC;


										-- LEVEL 3: Advanced Analysis (13–17)
-- Who is the highest-paid employee in each department?

WITH highest_paid AS
(select Name,Department,salary,
ROW_NUMBER() OVER(Partition BY Department ORDER BY SALARY DESC,Name ASC) rn
FROM employees)
select Name,
Department,
Salary 
from highest_paid
WHERE rn=1;

Select Name,Department,Salary 
FROM (SELECT 
Name,
Department,
salary,
ROW_NUMBER() OVER(Partition BY Department ORDER BY SALARY DESC,Name ASC) rn
FROM employees) T1
WHERE rn=1;

-- List the top 3 highest-paid employees in each department.
 WITH highest_paid AS
(select 
Name,
Department,
salary,
ROW_NUMBER() OVER(Partition BY Department ORDER BY SALARY DESC) rn
FROM employees)
select Name,
Department,
Salary 
from highest_paid
WHERE rn<=3;

-- Find employees whose salary is greater than the company-wide average salary.
select Name,salary
FROM employees
WHERE salary > 
(select ROUND(avg(salary),2) 
						avg_salary FROM employees);


-- Calculate the salary difference (maximum salary − minimum salary) for each department.

Select Department,
(Max(salary)-MIN(Salary)) salary_diff
from employees
GROUP BY Department;

-- Count the number of employees with more than 5 years of experience.
select count(emp_id) total_emp
FROM employees
WHERE exp>5

This project strengthened my understanding of SQL by applying database management, data cleaning, aggregation, subqueries, and window functions to solve practical HR business problems. It serves as a foundational portfolio project for a Data Analyst role.
