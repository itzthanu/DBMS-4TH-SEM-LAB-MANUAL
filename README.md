Create a table called Employee with the following structure. Name Data Type Empno Number Ename Varchar(20) Job Varchar(20) Mgr_no Number Salary Number 
a) Create a table Employee 
b) Add Primary Key constraints and Not Null Constraints to the employee table 
c) Add a column commission with domain to the Employee table. 
d) Insert any five records into the table. 
e) Update the column details of job. 
f) Rename the column of Employee table using alter command. 
g) Delete the employee whose empno is 105.
 h) Find salaries of employee in Ascending Order.
 i) Find grouped salaries of employees.

 
SOLUTION:
A)	CREATE DATABASE EMPLOYEE_DETAILS
USE EMPLOYEE_DETAILS

B)	CREATE TABLE EMPLOYEE(EMPNO NUMBER PRIMARY KEY ,ENAME VARCHAR(20) NOTNULL,JOB VARCHAR(20) NOTNULL,MRG_NO NUMBER NOTNULL,SALARY NUMBER NOTNULL);

C)	ALTER TABLE EMPLOYEE
ADD COMMISSION NUMBER;

D)	INSERT INTO EMPLOYEE VALUES(‘101’,’ALICE’,’DESIGNER’,001,50000);
INSERT INTO EMPLOYEE VALUES(‘102’,’BOB’,’ANALYST’,001,60000);
INSERT INTO EMPLOYEE VALUES(‘103’,’CLAV’,’HR’,001,90000);
INSERT INTO EMPLOYEE VALUES(‘104’,’DAN’,’DEVELOPER’,001,70000);
INSERT INTO EMPLOYEE VALUES(‘105’,’ELON’,’SENIOR DESIGNER’,001,50000);

E)	UPDATE EMPLOYEE
SET JOB=”DEVELOPER”
WHERE EMPNO=’104’;

F)	ALTER TABLE EMPLOYEE
RENAME COLUMN MGR_NO, MANAGER_NO;
G)	DELETE FROM EMPLOYEE
WHERE EMPNO=’105’;

H)	SELECT SALARY
FROM EMPLOYEE
ORDER BY SALARY ALL;

I)	SELECT SALARY,COUNT(*)
FROM EMPLOYEE
GROUP BY SALARY;


