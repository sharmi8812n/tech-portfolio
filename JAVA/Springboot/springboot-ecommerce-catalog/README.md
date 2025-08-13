# 🛍️ Spring Boot E-Commerce Product Catalogue (Java 8)

A REST API for managing an eCommerce product catalogue.

## Features
- Add, view, update, delete products
- Data validation
- In-memory H2 database

## Tech Stack
- Java 8
- Spring Boot 2.7.x
- Spring Data JPA
- H2 Database
- Lombok

## How to Run
```bash
mvn spring-boot:run
```

## API Endpoints
| Method | Endpoint        | Description         |
|--------|----------------|---------------------|
| GET    | `/api/products` | Get all products    |
| GET    | `/api/products/{id}` | Get product by ID |
| POST   | `/api/products` | Add new product     |
| PUT    | `/api/products/{id}` | Update product    |
| DELETE | `/api/products/{id}` | Delete product    |
