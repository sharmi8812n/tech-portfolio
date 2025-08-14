### Oracle PL/SQL Cheat Sheet with Command Uses
## 1. PL/SQL Block Structure
DECLARE
  -- Declare variables here
BEGIN
  -- Procedural code here
EXCEPTION
  -- Exception handling here
END;
/

Use: Structure of a PL/SQL program block — declare variables, write code, and handle errors.

## 2. Variable Declaration
DECLARE
  v_name VARCHAR2(50);
  v_salary NUMBER(8,2);
  v_hire_date DATE;
BEGIN
  -- code
END;
/
Use: Define variables with types to store and manipulate data.

## 3. Assigning Values
v_name := 'John Doe';
v_salary := 4500.50;
v_hire_date := SYSDATE;
Use: Assign values to variables.

## 4. Control Flow

IF Statement
IF v_salary > 5000 THEN
  DBMS_OUTPUT.PUT_LINE('High salary');
ELSIF v_salary > 3000 THEN
  DBMS_OUTPUT.PUT_LINE('Medium salary');
ELSE
  DBMS_OUTPUT.PUT_LINE('Low salary');
END IF;

Use: Conditional branching based on conditions.

CASE Statement
CASE v_priority
  WHEN 'HIGH' THEN DBMS_OUTPUT.PUT_LINE('Urgent task');
  WHEN 'MEDIUM' THEN DBMS_OUTPUT.PUT_LINE('Normal priority');
  ELSE DBMS_OUTPUT.PUT_LINE('Low priority');
END CASE;
Use: Multi-way branching.

LOOP
FOR i IN 1..10 LOOP
  DBMS_OUTPUT.PUT_LINE('Count: ' || i);
END LOOP;
Use: Repeat code a fixed number of times.

WHILE LOOP
WHILE v_counter < 10 LOOP
  DBMS_OUTPUT.PUT_LINE('Counter: ' || v_counter);
  v_counter := v_counter + 1;
END LOOP;
Use: Repeat code while a condition holds.

## 5. Cursors

Implicit Cursor
DECLARE
  v_salary NUMBER;
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE employee_id = 101;
  DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
END;
/
Use: Simple query retrieving single row into a variable.

Explicit Cursor
DECLARE
  CURSOR c_emp IS SELECT employee_id, first_name FROM employees;
  v_emp c_emp%ROWTYPE;
BEGIN
  OPEN c_emp;
  LOOP
    FETCH c_emp INTO v_emp;
    EXIT WHEN c_emp%NOTFOUND;
    DBMS_OUTPUT.PUT_LINE('Employee: ' || v_emp.employee_id || ', ' || v_emp.first_name);
  END LOOP;
  CLOSE c_emp;
END;
/
Use: Fetch multiple rows one at a time.

## 6. Exception Handling
BEGIN
  -- code that might fail
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    DBMS_OUTPUT.PUT_LINE('No data found!');
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
END;
/
Use: Handle runtime errors gracefully.

## 7. Procedures
CREATE OR REPLACE PROCEDURE greet_user(p_name IN VARCHAR2) AS
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello, ' || p_name);
END;
/
Use: Named blocks of code that perform actions, can accept parameters.

## 8. Functions
CREATE OR REPLACE FUNCTION get_salary(p_emp_id IN NUMBER) RETURN NUMBER AS
  v_salary NUMBER;
BEGIN
  SELECT salary INTO v_salary FROM employees WHERE employee_id = p_emp_id;
  RETURN v_salary;
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    RETURN NULL;
END;
/
Use: Named blocks that return a value.

## 9. Calling Procedures and Functions
BEGIN
  greet_user('Alice');
  DBMS_OUTPUT.PUT_LINE('Salary: ' || get_salary(101));
END;
/
Use: Execute procedures/functions.

## 10. Packages

Specification

CREATE OR REPLACE PACKAGE emp_pkg AS
  PROCEDURE add_employee(p_name VARCHAR2, p_salary NUMBER);
  FUNCTION get_salary(p_emp_id NUMBER) RETURN NUMBER;
END emp_pkg;
/
Use: Declare grouped procedures and functions.

Body

CREATE OR REPLACE PACKAGE BODY emp_pkg AS

  PROCEDURE add_employee(p_name VARCHAR2, p_salary NUMBER) IS
  BEGIN
    INSERT INTO employees (first_name, salary) VALUES (p_name, p_salary);
  END;

  FUNCTION get_salary(p_emp_id NUMBER) RETURN NUMBER IS
    v_salary NUMBER;
  BEGIN
    SELECT salary INTO v_salary FROM employees WHERE employee_id = p_emp_id;
    RETURN v_salary;
  EXCEPTION
    WHEN NO_DATA_FOUND THEN
      RETURN NULL;
  END;

END emp_pkg;
/
Use: Define the actual implementation of package members.

## 11. Triggers
CREATE OR REPLACE TRIGGER trg_before_insert_employee
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  :NEW.hire_date := SYSDATE;
END;
/
Use: Automatically execute code on data changes (insert/update/delete).

## 12. DBMS_OUTPUT
DBMS_OUTPUT.PUT_LINE('Message here');
Use: Print output from PL/SQL for debugging/logging.

Make sure to enable output in SQL*Plus with:
SET SERVEROUTPUT ON;
