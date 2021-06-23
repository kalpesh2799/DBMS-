# DBMS-
Import the database humanresource
source (path\filename.sql)
************************************************************************************************************************
			"All SQL syntax quries Knowledge within single repo"
*************************************************************************************************************************
1) Display all the employee whose salary greater then average salary of there department. 

-->select first_name,salary from emp where salary > (select avg(salary) from emp where department_id=20);


2) Display employees where length of ename is 5
-->select * from employees where LENGTH(first_name)>5;

3) Display all employees where ename start with J and ends with S
-->select first_name from emp where first_name like "j%";

4) Display all employees where employee does not belong to 10,20,40 department_id
-->SELECT * FROM employees WHERE DEPARTMENT_ID NOT IN (10,20,40);

5)Display all employees where jobs does not belong to PRESIDENT and MANAGER?
->select * from employees where (select * from jobs where UPPER(JOB_TITLE) Like "%PRESIDENT%" OR UPPER(JOB_TITLE) "%MANAGER%");

6) Display all three figures salary in emp table
-->`select * from employees where salary>99 and salary>=999; 

7) Display all records in emp table for employee who does not receive any commission
-->select * from employees where (COMMITION_PCT	is NULL) or COMMITION_PCT=0;

8) Display all ename where first character could be anything, but
second character should be L?
-->SELECT * FROM employees WHERE UPPER(SUBSTR(FIRST_NAME,2,1))='L';

9) Display nth highest and nth lowest salary in emp table?
-->i)select first_name min(salary),max(salary) from emp;

10) Display all the departments where department has 3 employees?
-->  SELECT DEPARTMENT_ID,COUNT(*),(SELECT DEPARTMENT_NAME FROM
DEPARTMENTS D WHERE D.DEPARTMENT_ID=E.DEPARTMENT_ID) AS DEPTNAME
FROM employees E GROUP BY DEPARTMENT_ID HAVING (COUNT(*))=3
 
11) Display emp name and corresponding subordinates. Use CONNECT BY clause.
-->

12) Display all ename, sal, deptno,dname from emp, dept table where all department which has employees as well as department does not have any employees. This query should include non matching rows.
-->select * from first_name,salary,deptno,department_name form empoyees e left join departments d ON e.department_id=d.department_id
		union
select * from first_name,salary,deptno,department_name form empoyees e right join departments d ON e.department_id=d.department_id
	 

13) Display all ename, sal, deptno from emp, dept table where all employees which has matching department as well as employee does not have any departments. This query should include non matching rows.
-->select * from first_name,salary,deptno,department_name form empoyees e left join departments d ON e.department_id=d.department_id
		union
select * from first_name,salary,deptno,department_name form empoyees e right join departments d ON e.department_id!=d.department_id

Note: In the below query, employee will always have matching record in dept table. Emp, dept table may not be good example to answer this question.


14) Display all ename, sal, deptno from emp, dept table where all employees which has matching and non matching department as well as all departments in dept table which has matching and non matching employees. This query should include non matching rows on both the tables. 
-->select * from first_name,salary,deptno,department_name form empoyees e left join departments d ON e.department_id=d.department_id
		union
select * from first_name,salary,deptno,department_name form empoyees e right join departments d ON e.department_id=d.department_id


Note: In the below query, employee will always have matching record in dept table. Emp, dept table may not be good example to answer this question.

15) Display all ename, empno, dname, loc from emp, dept table without joining two tables
-->select e.employee_id,e.first_name, d.department_name, l.street_address,
l.postal_code, l.city from employees e, departments d, locations l
where e.department_id=d.department_id
and d.location_id= l.location_id;

16) Display all the departments where department does not have any employees
-->SELECT DEPARTMENT_ID,COUNT(*),(SELECT DEPARTMENT_NAME FROM
DEPARTMENTS D WHERE D.DEPARTMENT_ID=E.DEPARTMENT_ID) AS DEPTNAME
FROM employees E GROUP BY DEPARTMENT_ID HAVING (COUNT(*))=0;

17) Display all the departments where department does have atleast one employee
-->SELECT DEPARTMENT_ID,COUNT(*) as EmployeeCount,(SELECT
DEPARTMENT_NAME FROM DEPARTMENTS D WHERE
D.DEPARTMENT_ID=E.DEPARTMENT_ID) AS DEPTNAME
FROM employees E GROUP BY DEPARTMENT_ID HAVING (COUNT(*))>=1;

18) Display all employees those who are not managers?
-->select * from employees where job_id not in (select job_id from jobs where job_title
like '%manager%');

19) Display ename, deptno from emp table with format of {ename} belongs to {deptno}
-->elect first_name,Last_name,(select department_name from departments d where
e.department_id=d.department_id) as DEPTNAME from employees e;

20) Display total number of employees hired for 1980,1981,1982. The output should be in one record.
-->SELECT COUNT(*) FROM employees where YEAR(HIRE_DATE) IN (1980,1981,1982);

21) Display ename, deptno from employee table. Also add another column in the same query and it should display ten for dept 10, twenty for dept 20, thirty for dept 30, fourty for dept 40
-->case
when DEPARTMENT_ID =10 then 'Ten'
when DEPARTMENT_ID =20 then 'Twenty'
when DEPARTMENT_ID =30 then 'Thirty'
when DEPARTMENT_ID =40 then 'Fourty'
when DEPARTMENT_ID =50 then 'Fifty'
when DEPARTMENT_ID =60 then 'Sixty'
when DEPARTMENT_ID =70 then 'Seventy'
when DEPARTMENT_ID =80 then 'Eighty'
when DEPARTMENT_ID =90 then 'Ninety'
when DEPARTMENT_ID =100 then 'Hundred'
else 'Another value'
end as DepartmentValue
FROM EMPLOYEES;


22) Display all the records in emp table. The ename should be lower case. The job first character should be upper case and rest of the character in job field should be lower case.
-->lower(first_name) ,


23) Display all employees those who have joined in first week of the month ?
-->select
lower(first_name),concat(upper(substr(job_id,1,1)),lower(substr(job_id,2,length(job_id
)))) from employees;


24) Display all empoyees those who have joined in the 49th week of the year?
-->select * from employees where week(hire_date)=49;

25) Display empno, deptno, salary, salary difference between current record and previous record in emp table. Deptno should be in descending order.
-->select e.employee_id,e.department_id,e.salary,(e.salary-e1.salary)
from employees e
inner join employees e1
on e1.employee_id = e.employee_id +1
order by department_id desc;


26) Create table emp1 and copy the emp table for deptno 10 while creating the table
-->create table emp1 as (select * from employees where department_id=10);


27) Create table emp2 with same structure of emp table. Do not copy the data
--> create table emp2 as SELECT * FROM EMPLOYEES where 1=2;


28) Insert new record in emp1 table, Merge the emp1 table on emp table.
-->insert into employees select * from emp1 where employee_id not in (select
employee_id from employees);

29) Display all the records for deptno which belongs to employee name JAMES? 
-->select * from employees WHERE DEPARTMENT_ID IN (select
DISTINCT(DEPARTMENT_ID) from employees where UPPER(first_name)='JAMES');

30) Display all the records in emp table where salary should be less then or equal to ADAMS salary?
-->sselect * from employees WHERE SALARY < (select DISTINCT(SALARY) from
employees where UPPER(first_name)='ADAM');

31) Display all employees those were joined before employee WARD joined?
-->
 select * from employees WHERE HIRE_DATE < (select DISTINCT(HIRE_DATE) from
employees where UPPER(first_name)='WINSTON';
32) Display all subordinate those who are working under BLAKE?
-->select * from employees WHERE MANAGER_ID IN ( select EMPLOYEE_ID from
employees WHERE UPPER(FIRST_NAME)='NEENA');

33) Display all subordinate(all levels) for employee BLAKE?
-->

34) Display all record in emp table for deptno which belongs to KING's Job? 
-->select * from employees WHERE DEPARTMENT_ID IN (SELECT DEPARTMENT_ID
from employees WHERE UPPER(LAST_NAME)='KING');

35) Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules that, salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.
-->SET SALARY= case when DEPARTMENT_ID =40 then SALARY*1.25
when DEPARTMENT_ID =90 then SALARY*1.15
when DEPARTMENT_ID =110 then SALARY*1.10
else SALARY
end;

36) Display list of ename those who have joined in Year 81 as MANAGER?
-->SELECT * FROM employees WHERE JOB_ID IN (select JOB_ID from JOBS WHERE
UPPER(JOB_TITLE) LIKE '%MANAGER%')
AND YEAR(hire_date)='1981'

37) Display who is making highest commission?
-->
SELECT * FROM employees WHERE commission_pct = (SELECT
MAX(commission_pct) FROM EMPLOYEES);

38) Display who is senior most employee? How many years has been working?
-->
SELECT
EMPLOYEE_ID,first_name,last_name,hire_date,(YEAR(curdate())-YEAR(hire_date)) AS
EXPERIENCE FROM employees
WHERE hire_date= (SELECT MIN(hire_date) FROM employees)

39) Display who is most experienced and least experienced employee?
-->
SELECT * FROM EMPLOYEES WHERE hire_date = (SELECT MIN(hire_date) FROM
employees)
OR hire_date = (SELECT MAX(HIRE_DATE) FROM EMPLOYEES)


40) Display ename, sal, grade, dname, loc for each employee.
-->
SELECT concat(FIRST_NAME,' ',LAST_NAME) AS ENAME,SALARY,
D.DEPARTMENT_NAME,L.city AS LOC
FROM employees E
INNER JOIN DEPARTMENTS D ON E.department_id = D.department_id
INNER JOIN locations L ON L.location_id = D.location_id;

41) Display all employee whose location is DALLAS?
-->
SELECT concat(FIRST_NAME,' ',LAST_NAME) AS ENAME,SALARY,
D.DEPARTMENT_NAME,L.state_province AS LOC
FROM employees E
INNER JOIN DEPARTMENTS D ON E.department_id = D.department_id
INNER JOIN locations L ON L.location_id = D.location_id AND
UPPER(L.state_province)='TEXAS';

42) Display ename, job, dname, deptno for each employee by using INLINE view?
-->SELECT concat(FIRST_NAME,' ',LAST_NAME) AS ENAME,SALARY,
job_id,department_id,
(SELECT department_NAME FROM DEPARTMENTS D where
D.department_id=E.department_id) AS DNAME
FROM employees E;

43) List ename, job, sal and department of all employees whose salary is not within the salary grade?
-->SELECT concat(FIRST_NAME,' ',LAST_NAME) AS ENAME,SALARY,
D.DEPARTMENT_NAME,J.MIN_SALARY,J.MAX_SALARY
FROM employees E
INNER JOIN DEPARTMENTS D ON E.department_id = D.department_id
INNER JOIN JOBS J ON J.job_id = E.job_id AND (SALARY < MIN_SALARY OR
SALARY > MAX_SALARY); 

44)Use EMP and EMP1 table. Query should have only three columns. Display empno,ename,sal from both tables inluding duplicates. 
-->SELECT E.EMPLOYEE_ID, E.first_name,E.last_name,E.SALARY
FROM employees E
union
SELECT E1.EMPLOYEE_ID, E1.first_name,E1.last_name,E1.SALARY
FROM emp1 E1;

45) Display the employees for empno which belongs to job PRESIDENT?
-->SELECT * FROM employees WHERE MANAGER_ID IN(select EMPLOYEE_ID from employees
WHERE JOB_ID IN
(select JOB_ID from JOBS WHERE UPPER(JOB_TITLE) LIKE '%PRESIDENT%')
