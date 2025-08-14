# MySQL on Windows - README

## Overview
MySQL is a popular open-source relational database system. This guide helps you install and get started with MySQL on Windows.

---

## Features
- Reliable, fast, and easy to use
- Supports ACID transactions
- Stored procedures, triggers, views
- Scalable and secure
- Integration with many programming languages and tools

---

## Installation on Windows

### Step 1: Download Installer
- Go to [MySQL Downloads](https://dev.mysql.com/downloads/installer/)
- Choose **MySQL Installer for Windows** (web or full version)

### Step 2: Run Installer
- Launch the downloaded installer `.msi` file
- Select **Setup Type**:
  - Developer Default (recommended for developers)
  - Server only
  - Client only
  - Custom (choose components manually)
- Click **Next**

### Step 3: Installation Process
- The installer will download and install required components
- Follow prompts and accept license agreements
- Configure MySQL Server:
  - Choose Config Type (Development, Server, Dedicated)
  - Set root password (remember this)
  - Optionally create user accounts
  - Set port (default 3306)
- Complete installation

### Step 4: Verify Installation
- Open **Command Prompt**
- Run:
  ```bash
  mysql -u root -p


Basic Usage
Start MySQL Server (if not running)

MySQL runs as a Windows service by default

To start/stop service:

Open Services app (services.msc)

Find MySQL service and start/stop it

Connect to MySQL Shell
mysql -u root -p

Common Commands
Create Database
CREATE DATABASE testdb;

Use Database
USE testdb;

Create Table
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50) NOT NULL,
  email VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Insert Data
INSERT INTO users (username, email) VALUES ('alice', 'alice@example.com');

Query Data
SELECT * FROM users;

Exit MySQL Shell
EXIT;
