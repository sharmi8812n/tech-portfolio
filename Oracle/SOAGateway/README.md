## EmployeeServiceGateway - SOA Gateway Sample Project

## Overview
This project demonstrates a simple Employee Management Service using SOA Gateway. The service allows you to:
    Get employee details by ID
    Add a new employee
    Update an employee's salary
The SOA Gateway acts as a middleware layer exposing backend services (like databases or SOAP services) as REST or SOAP endpoints, making integration with external systems seamless.

## What is SOA Gateway?
    SOA Gateway is part of Oracle SOA Suite.
    It enables you to expose business logic as standardized web services (REST or SOAP).
    Provides routing, transformation, and orchestration between different systems.
    Allows easy integration of backend applications (databases, ERP, legacy systems) with modern consumers.

## Tech Stack
    Oracle SOA Suite 12c / SOA Cloud Service
    Oracle Database 19c
    JDeveloper / SOA Studio
    REST & SOAP services

<img width="913" height="347" alt="image" src="https://github.com/user-attachments/assets/15d91e8b-e0f4-4038-928e-f9e5ab109759" />

## Setup Instructions

1. Database Setup
    Connect to your Oracle Database using SQL*Plus or SQL Developer.
    Execute the scripts in order:
    @db_scripts/create_employees_table.sql
    @db_scripts/sample_data.sql
    Verify that the employees table has sample data.

2. SOA Composite Deployment
    Open JDeveloper or SOA Studio.
    Import soa_composite/EmployeeServiceGateway.jar.
    Deploy the composite to your SOA Server or SOA Cloud Service.
    Ensure the composite is active.

3. Testing REST Endpoint

Use Postman or SOAP UI to test the REST endpoints.
Example requests:

GET Employee by ID
    GET http://<soa-server>:7001/EmployeeServiceGateway/employees/1001
    POST New Employee
    POST http://<soa-server>:7001/EmployeeServiceGateway/employees
    Body (JSON):
    {
      "employee_id": 1003,
      "name": "Alice Johnson",
      "department": "Finance",
      "salary": 7000
    }

PUT Update Salary
    PUT http://<soa-server>:7001/EmployeeServiceGateway/employees/1001/salary
    Body (JSON):
    {
      "salary": 5500
    }

A Postman collection is provided in postman_collection/ for testing.
