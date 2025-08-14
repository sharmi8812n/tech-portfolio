# Oracle Database - README

## Overview
Oracle Database is a powerful, enterprise-grade relational database management system (RDBMS) widely used for mission-critical applications. It offers advanced features for data storage, retrieval, security, and high availability.

---

## Features
- Supports SQL and PL/SQL for data manipulation and programming
- ACID compliant transactions for data integrity
- Advanced indexing and partitioning
- Data replication and clustering (RAC)
- Security features including encryption and auditing
- Support for large data volumes and complex queries
- Advanced SQL Support:** Comprehensive SQL compliance with PL/SQL for procedural programming.
- High Availability:** Features like Real Application Clusters (RAC), Data Guard for failover.
- Scalability:** Supports large databases, multi-tenant architectures.
- Security:** Robust access control, encryption, auditing.
- Performance:** Optimized query processing, indexing, partitioning.
- Data Warehousing & Analytics:** Built-in tools for data analytics and reporting.
- Backup and Recovery:** Efficient tools for backup, restore, and disaster recovery.
- Support for JSON, XML, Spatial Data, and more.**

---

## Setup & Installation

### Prerequisites
- Supported Operating System (Windows, Linux, Solaris, etc.)
- Sufficient disk space and memory (depends on edition)
- Oracle JDK for development if using Java apps

### Installation Steps
1. Download Oracle Database software from [Oracle Downloads](https://www.oracle.com/database/technologies/)
2. Run installer and follow guided setup instructions
3. Create and configure your database instance (use DBCA - Database Configuration Assistant)
4. Set environment variables (e.g., ORACLE_HOME, PATH)

---

## Connecting to Oracle DB

- Using SQL*Plus CLI:
  ```bash
  sqlplus username/password@host:port/SID

---

## Using Oracle Database with Java Spring Boot

### 1. Add Oracle JDBC Driver Dependency

Oracle’s JDBC driver is typically not available on public Maven repos due to licensing. You need to manually add it or use Oracle’s Maven repo.
<!-- Example if added to local repo -->
<dependency>
  <groupId>com.oracle.database.jdbc</groupId>
  <artifactId>ojdbc8</artifactId>
  <version>19.3.0.0</version>
</dependency>

### 2. Configure Spring Boot application.properties or application.yml
spring.datasource.url=jdbc:oracle:thin:@//localhost:1521/orclpdb1
spring.datasource.username=your_db_username
spring.datasource.password=your_db_password
spring.datasource.driver-class-name=oracle.jdbc.OracleDriver

spring.jpa.database-platform=org.hibernate.dialect.Oracle12cDialect
spring.jpa.hibernate.ddl-auto=update

### 3. Sample Entity and Repository
@Entity
public class Task {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  private String title;
  private String description;

  // getters & setters
}

public interface TaskRepository extends JpaRepository<Task, Long> {
}

### 4. Basic Service & Controller

Use standard Spring Data JPA repository methods to interact with Oracle database.

