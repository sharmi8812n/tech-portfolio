# PostgreSQL SQL

## Overview
PostgreSQL is a powerful, open-source object-relational database system known for its robustness, extensibility, and standards compliance.

---

## Features
- ACID-compliant transactions
- Advanced data types (JSON, arrays, UUID, etc.)
- MVCC for concurrent access
- Support for procedural languages (PL/pgSQL)
- Extensible indexing and full-text search
- Strong community and frequent updates

---

## Setup & Installation

### Prerequisites
- Supported OS (Linux, Windows, macOS)
- 1 GB RAM minimum recommended

### Installation
- On Ubuntu/Debian:
  ```bash
  sudo apt update
  sudo apt install postgresql postgresql-contrib

1. Connecting to PostgreSQL
psql -h hostname -p port -U username -d database
Use: Connect to a PostgreSQL database from command line.

2. Basic Data Retrieval
SELECT * FROM employees;
Use: Retrieve all rows and columns from the employees table.

SELECT first_name, last_name FROM employees WHERE department_id = 10;
Use: Retrieve specific columns with a filter.

4. Insert Data
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES (101, 'John', 'Doe', CURRENT_DATE);
Use: Add a new row to a table; CURRENT_DATE inserts current date.

4. Update Data
UPDATE employees SET salary = salary * 1.1 WHERE employee_id = 101;
Use: Modify existing rows (e.g., increase salary by 10%).

5. Delete Data
DELETE FROM employees WHERE employee_id = 101;
Use: Remove rows from a table based on condition.

6. Create Table
CREATE TABLE tasks (
  task_id SERIAL PRIMARY KEY,
  title VARCHAR(100),
  description TEXT,
  due_date DATE,
  status VARCHAR(20)
);
Use: Define a new table with columns and constraints. SERIAL auto-increments.

7. Alter Table
ALTER TABLE tasks ADD COLUMN priority VARCHAR(10);
Use: Add a new column to an existing table.

ALTER TABLE tasks DROP COLUMN priority;
Use: Remove a column from a table.

9. Drop Table
DROP TABLE tasks;
Use: Permanently delete a table and its data.

9. Constraints

Primary Key
ALTER TABLE employees ADD CONSTRAINT emp_pk PRIMARY KEY (employee_id);
Use: Enforce uniqueness and identify each row uniquely.

Foreign Key
ALTER TABLE employees ADD CONSTRAINT dept_fk FOREIGN KEY (department_id)
REFERENCES departments(department_id);
Use: Ensure referential integrity between tables.

Unique
ALTER TABLE employees ADD CONSTRAINT email_uk UNIQUE (email);
Use: Ensure column values are unique across rows.

10. Joins
SELECT e.first_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.department_id;
Use: Combine rows from two tables where related.

SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id;
Use: Retrieve all employees even if they have no department.

11. Aggregate Functions
SELECT department_id, COUNT(*) AS employee_count, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 5000;
Use: Summarize data by groups; filter groups with HAVING.

12. Sequences and Serial

Create Sequence
CREATE SEQUENCE task_seq START 1 INCREMENT 1;
Use: Generate unique incremental numbers.

Use Sequence
INSERT INTO tasks (task_id, title) VALUES (nextval('task_seq'), 'New Task');
Note: Usually, SERIAL type auto-manages sequences.

13. Transactions
BEGIN;
-- SQL statements

COMMIT;
Use: Start and commit a transaction.

ROLLBACK;
Use: Undo transaction.

14. Data Types
Data Type	Use
INTEGER	Whole numbers
SERIAL	Auto-increment integer
VARCHAR(n)	Variable length string
TEXT	Large text
DATE	Date values
TIMESTAMP	Date and time
BOOLEAN	True/False

16. Useful Meta-Commands (psql)
\d                      -- List tables
\d table_name            -- Describe table structure
\dt                     -- List tables only
\di                     -- List indexes
\df                     -- List functions
\l                      -- List databases

Use: Quick metadata commands inside psql shell.

16. Views
CREATE VIEW active_employees AS
SELECT * FROM employees WHERE status = 'Active';
Use: Create a virtual table for commonly used queries.

17. Functions
CREATE OR REPLACE FUNCTION get_employee_salary(emp_id INT) RETURNS NUMERIC AS $$
DECLARE
  salary NUMERIC;
BEGIN
  SELECT salary INTO salary FROM employees WHERE employee_id = emp_id;
  RETURN salary;
END;
$$ LANGUAGE plpgsql;
Use: Create reusable functions with procedural logic.

18. Triggers
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON employees
FOR EACH ROW
EXECUTE FUNCTION update_modified_column();
Use: Run code automatically on table changes.
