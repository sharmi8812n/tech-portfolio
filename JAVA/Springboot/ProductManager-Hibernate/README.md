# 📦 ProductManager – Spring Boot CRUD Application

A complete **Spring Boot** sample application for managing products, built using **Spring MVC**, **Spring Data JPA (Hibernate)**, **Thymeleaf**, and **MySQL**.  
It demonstrates how to perform basic **CRUD** (Create, Read, Update, Delete) operations in a layered architecture using modern Java web development practices.

## 🔍 Overview
This project is a **Product Management** application that allows users to:
- Create new products
- View all products
- Edit product details
- Delete products

It uses:
- **Spring Boot** for application bootstrapping
- **Spring MVC** for request handling
- **Spring Data JPA** with Hibernate for database persistence
- **Thymeleaf** for server-side HTML rendering

---

## ✨ Features
- **CRUD Operations**: Add, edit, view, delete products
- **Database Integration**: Persistent data storage using MySQL
- **Template Rendering**: Thymeleaf templates for clean UI
- **ORM Mapping**: Hibernate to map Java objects to database tables
- **Layered Architecture**: Controller → Service → Repository

---

## 🏗 Architecture

```text
+-------------+        +-------------+        +--------------+        +------------+
|  Controller | -----> |   Service   | -----> |  Repository  | -----> |  Database  |
+-------------+        +-------------+        +--------------+        +------------+
       |                     |                       |
     Thymeleaf Views      Business Logic         JPA / Hibernate

