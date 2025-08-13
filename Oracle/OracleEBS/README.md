# Oracle EBS Employee & Payroll Sample Project

## Overview
This project demonstrates HRMS and Payroll functionality in Oracle E-Business Suite. It includes sample employees, departments, jobs, payroll run, and reports.
## Tech Stack
    Oracle E-Business Suite 12.2.x
    Oracle Database 19c
    PL/SQL / SQL Loader for data import
    Optional: Oracle Integration Cloud for syncing data


## Modules Used:
    HRMS – Human Resources Management System
    Payroll – Process employee salaries
    Accounts Payable (AP) – Record payroll payments

## Processes:
    Create sample employees in HRMS
    Assign them to departments and jobs
    Run payroll calculation
    Post payroll journal entries to AP
    Generate payroll reports

## Setup Instructions

1. Import data:
   - Use HRMS Quick Entry or SQL scripts in `sql_scripts/` to create employees, departments, and jobs.
2. Run payroll:
   - Follow instructions in `payroll/payroll_run_instructions.txt`.
3. Generate reports:
   - Use standard EBS reports to view employee and payroll data.

## Integration (Optional)
- Connect with Oracle Integration Cloud (OIC) to sync employee/payroll data with external systems.
  
<img width="732" height="607" alt="image" src="https://github.com/user-attachments/assets/207815ed-f1d4-4487-b361-c25186610784" />

Setup Instructions
1. Prerequisites
    A running Oracle EBS instance (Cloud or On-Premises)
    HRMS and Payroll modules enabled
    System Administrator privileges in EBS

2. Import Sample Data
    You have two options:
    Option A: Using CSV/Quick Entry in HRMS
    Login to EBS with HRMS responsibility.
    Navigate to Employees → Enter Employees.
    Create sample employees using data/employees.csv.
    Similarly, create departments (departments.csv) and jobs (jobs.csv).
    Option B: Using SQL Scripts
    Open a SQL client connected to the EBS database.
    Run the scripts in the following order:
    sql_scripts/load_departments.sql
    sql_scripts/load_jobs.sql
    sql_scripts/load_employees.sql

Verify that the data appears in the corresponding tables.

3. Run Payroll
    Login to EBS HRMS / Payroll module.
    Navigate to Payroll → Define Payroll → Run Payroll.
    Select sample employees.
    Validate the payroll.
    Post the payroll to generate accounting entries.
    Generate payslips and save for reference.

4. Generate Reports
    Employee List Report: Navigate to Reports → Standard Reports → Employee List
    Payroll Journal Report: Navigate to Reports → Standard Reports → Payroll Journal
    Payslips: Generated from payroll run

