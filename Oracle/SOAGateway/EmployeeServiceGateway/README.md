# EmployeeServiceGateway - SOA Gateway Sample Project

## Overview
This project demonstrates a simple Employee Management service using **Oracle SOA Gateway**. It exposes REST and SOAP endpoints to perform basic operations on employee data.

## Tech Stack
- Oracle SOA Suite 12c / SOA Cloud Service
- Oracle Database 19c
- JDeveloper / SOA Studio
- REST & SOAP services

## Setup Instructions

1. **Database Setup**
   - Run `db_scripts/create_employees_table.sql` to create table.
   - Run `db_scripts/sample_data.sql` to insert sample employees.

2. **SOA Composite Deployment**
   - Import `soa_composite/EmployeeServiceGateway.jar` into SOA Server or Cloud Service.
   - Deploy the composite.

3. **Testing REST Endpoint**
   - Use Postman or SOAP UI.
   - Example: GET `http://localhost:7001/EmployeeServiceGateway/employees/1001`

## Project Structure
```
EmployeeServiceGateway/
├── db_scripts/
├── soa_composite/
├── postman_collection/
└── README.md
```

