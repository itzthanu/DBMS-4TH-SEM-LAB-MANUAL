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

B)	CREATE TABLE EMPLOYEE (
    EMPNO INT PRIMARY KEY,
    ENAME VARCHAR(20) NOT NULL,
    JOB VARCHAR(20) NOT NULL,
    MGR_NO INT NOT NULL,
    SALARY DECIMAL(10, 2) NOT NULL
);


C)	ALTER TABLE EMPLOYEE
ADD COMMISSION NUMBER; OR
ALTER TABLE EMPLOYEE
ADD COMMISSION DECIMAL(10, 2);


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

OR

CREATE DATABASE EMPLOYEE_DETAILS;
USE EMPLOYEE_DETAILS;

CREATE TABLE EMPLOYEE (
    EMPNO INT PRIMARY KEY,
    ENAME VARCHAR(20) NOT NULL,
    JOB VARCHAR(20) NOT NULL,
    MGR_NO INT NOT NULL,
    SALARY DECIMAL(10, 2) NOT NULL
);

ALTER TABLE EMPLOYEE
ADD COMMISSION DECIMAL(10, 2);

INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR_NO, SALARY) VALUES (101, 'ALICE', 'DESIGNER', 001, 50000);
INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR_NO, SALARY) VALUES (102, 'BOB', 'ANALYST', 001, 60000);
INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR_NO, SALARY) VALUES (103, 'CLAV', 'HR', 001, 90000);
INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR_NO, SALARY) VALUES (104, 'DAN', 'DEVELOPER', 001, 70000);
INSERT INTO EMPLOYEE (EMPNO, ENAME, JOB, MGR_NO, SALARY) VALUES (105, 'ELON', 'SENIOR DESIGNER', 001, 50000);

UPDATE EMPLOYEE
SET JOB = 'DEVELOPER'
WHERE EMPNO = 104;

-- Adjust column renaming based on your DBMS:
ALTER TABLE EMPLOYEE
RENAME COLUMN MGR_NO TO MANAGER_NO;

DELETE FROM EMPLOYEE
WHERE EMPNO = 105;

SELECT SALARY
FROM EMPLOYEE
ORDER BY SALARY;

SELECT SALARY, COUNT(*)
FROM EMPLOYEE
GROUP BY SALARY;

2) Create cursor for Employee table & extract the values from the table. Declare the variables, Open 
the cursor & extrct the values from the cursor. Close the cursor.  
                       Employee (E_id, E_name, Age, Salary)
   SOLUTION
   CREATE TABLE Employee (
    E_id INT PRIMARY KEY,
    E_name VARCHAR(50),
    Age INT,
    Salary DECIMAL(10, 2)
);
DECLARE
    -- Declare variables to hold the values fetched from the cursor
    v_E_id Employee.E_id%TYPE;
    v_E_name Employee.E_name%TYPE;
    v_Age Employee.Age%TYPE;
    v_Salary Employee.Salary%TYPE;

    -- Declare the cursor
    CURSOR employee_cursor IS
        SELECT E_id, E_name, Age, Salary
        FROM Employee;

BEGIN
    -- Open the cursor
    OPEN employee_cursor;

    -- Fetch rows from the cursor
    LOOP
        FETCH employee_cursor INTO v_E_id, v_E_name, v_Age, v_Salary;
        EXIT WHEN employee_cursor%NOTFOUND;
        
        -- Process the data (For example, print to the console or other actions)
        DBMS_OUTPUT.PUT_LINE('ID: ' || v_E_id || ', Name: ' || v_E_name || ', Age: ' || v_Age || ', Salary: ' || v_Salary);
    END LOOP;

    -- Close the cursor
    CLOSE employee_cursor;
END;
/

3) Queries using aggregate functions(COUNT,AVG,MIN,MAX,SUM),Group by, Orderby.  
                       Employee(E_id, E_name, Age, Salary)  
 
1. Create Employee table containing all Records E_id, E_name, Age, Salary.  
2. Count number of employee names from employeetable  
3. Find the Maximum age from employee table.  
4. Find the Minimum age from employeetable.  
5. Find salaries of employee in Ascending Order.  
6. Find grouped salaries of employees.
7. 
SOLUTION:

   CREATE TABLE Employee (
    E_id INT PRIMARY KEY,
    E_name VARCHAR(50),
    Age INT,
    Salary DECIMAL(10, 2)
);

-- Sample data
INSERT INTO Employee (E_id, E_name, Age, Salary) VALUES (1, 'Alice', 30, 50000);
INSERT INTO Employee (E_id, E_name, Age, Salary) VALUES (2, 'Bob', 40, 60000);
INSERT INTO Employee (E_id, E_name, Age, Salary) VALUES (3, 'Charlie', 25, 55000);
INSERT INTO Employee (E_id, E_name, Age, Salary) VALUES (4, 'David', 35, 70000);
INSERT INTO Employee (E_id, E_name, Age, Salary) VALUES (5, 'Eve', 29, 65000);

SELECT COUNT(E_name) AS NumberOfEmployees
FROM Employee;

SELECT MAX(Age) AS MaxAge
FROM Employee;

SELECT MIN(Age) AS MinAge
FROM Employee;

SELECT Salary
FROM Employee
ORDER BY Salary ASC;

SELECT Salary, COUNT(*) AS NumberOfEmployees
FROM Employee
GROUP BY Salary
ORDER BY Salary;

4) Create a row level trigger for the customers table that would fire for INSERT or UPDATE or 
DELETE operations performed on the CUSTOMERS table. This trigger will display the salary 
difference between the old & new Salary.  
             CUSTOMERS (ID,NAME,AGE,ADDRESS,SALARY).

   SOLUTION:

   -- Create the CUSTOMERS table if it doesn't exist
CREATE TABLE CUSTOMERS (
    ID INT PRIMARY KEY,
    NAME VARCHAR(100),
    AGE INT,
    ADDRESS VARCHAR(255),
    SALARY DECIMAL(10, 2)
);

-- Insert sample data
INSERT INTO CUSTOMERS (ID, NAME, AGE, ADDRESS, SALARY) VALUES (1, 'Alice', 30, '123 Elm St', 50000);
INSERT INTO CUSTOMERS (ID, NAME, AGE, ADDRESS, SALARY) VALUES (2, 'Bob', 40, '456 Oak St', 60000);
INSERT INTO CUSTOMERS (ID, NAME, AGE, ADDRESS, SALARY) VALUES (3, 'Charlie', 25, '789 Pine St', 55000);
INSERT INTO CUSTOMERS (ID, NAME, AGE, ADDRESS, SALARY) VALUES (4, 'David', 35, '135 Maple St', 70000);
INSERT INTO CUSTOMERS (ID, NAME, AGE, ADDRESS, SALARY) VALUES (5, 'Eve', 29, '246 Birch St', 65000);

-- Drop the trigger if it already exists
IF OBJECT_ID('tr_customer_salary', 'TR') IS NOT NULL
    DROP TRIGGER tr_customer_salary;
GO

-- Create the trigger
CREATE TRIGGER tr_customer_salary
ON CUSTOMERS
AFTER INSERT, UPDATE, DELETE
AS
BEGIN
    SET NOCOUNT ON;

    -- For INSERT operation
    IF EXISTS (SELECT * FROM inserted)
    BEGIN
        IF NOT EXISTS (SELECT * FROM deleted)
        BEGIN
            -- Insert
            SELECT 'Inserted Record: New Salary = ' + CAST(i.SALARY AS VARCHAR(20))
            FROM inserted i;
        END
        ELSE
        BEGIN
            -- Update
            SELECT 'Updated Record: Old Salary = ' + CAST(d.SALARY AS VARCHAR(20)) +
                   ', New Salary = ' + CAST(i.SALARY AS VARCHAR(20)) +
                   ', Salary Difference = ' + CAST(i.SALARY - d.SALARY AS VARCHAR(20))
            FROM inserted i
            INNER JOIN deleted d ON i.ID = d.ID;
        END
    END
    
    -- For DELETE operation
    IF EXISTS (SELECT * FROM deleted)
    BEGIN
        SELECT 'Deleted Record: Old Salary = ' + CAST(d.SALARY AS VARCHAR(20))
        FROM deleted d;
    END
END;
GO





