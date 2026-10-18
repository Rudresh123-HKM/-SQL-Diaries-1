
SQL Diaries #2 - Department Top Three Salaries
Problem
Find employees who earn one of the top 3 unique salaries within their department.

My First Thought
I initially focused on joining the Employee and Department tables and sorting salaries department-wise

Key Learning

The phrase "Top 3 Unique Salaries" indicates that DENSE_RANK() is required.

Concepts Used
JOIN
CTE
DENSE_RANK()
PARTITION BY
Window Functions

Solution

WITH cte AS
(
SELECT
d.name AS Department,
e.name AS Employee,
e.salary AS Salary,
DENSE_RANK() OVER
(
PARTITION BY e.departmentId
ORDER BY e.salary DESC
) AS salary_rank
FROM Employee e
JOIN Department d
ON e.departmentId = d.id
)
SELECT
Department,
Employee,
Salary
FROM cte
WHERE salary_rank <= 3;

What I Learned

✅ Difference between ROW_NUMBER(), RANK(), and DENSE_RANK()

✅ How to solve Top-N per Group problems

✅ Importance of understanding "unique salaries"

