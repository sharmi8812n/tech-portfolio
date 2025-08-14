# Apache Cassandra - README

## Overview
Apache Cassandra is a highly scalable, distributed NoSQL database designed to handle large amounts of data across many commodity servers, providing high availability with no single point of failure.

---

## Features
- Distributed and decentralized architecture
- Fault-tolerant with replication and data partitioning
- Tunable consistency levels
- High write and read throughput
- Support for wide-column data model
- Built-in support for time-series and IoT data

---

## Setup & Installation

### Prerequisites
- Java 8 or higher installed
- Minimum 4GB RAM recommended

### Installation Steps

1. Download Cassandra from [https://cassandra.apache.org](https://cassandra.apache.org)
2. Extract the archive and navigate to the Cassandra folder
3. Start Cassandra server:
   bin/cassandra -f

1. Connect to Cassandra
cqlsh <hostname> <port>
Use: Open Cassandra Query Language shell to run commands.

2. Create Keyspace
CREATE KEYSPACE my_keyspace WITH replication = {
  'class': 'SimpleStrategy',
  'replication_factor': 3
};
Use: Create a namespace (database) with replication settings.

3. Use Keyspace
USE my_keyspace;
Use: Switch to the keyspace to run queries within it.

4. Create Table
CREATE TABLE users (
  user_id UUID PRIMARY KEY,
  first_name text,
  last_name text,
  email text
);
Use: Define a table with columns and primary key.

5. Insert Data
INSERT INTO users (user_id, first_name, last_name, email)
VALUES (uuid(), 'John', 'Doe', 'john.doe@example.com');
Use: Add a row to a table.

6. Select Data
SELECT * FROM users WHERE user_id = <some-uuid>;
Use: Retrieve rows by primary key (or indexed columns).

7. Update Data
UPDATE users SET email = 'new.email@example.com' WHERE user_id = <some-uuid>;
Use: Modify existing rows identified by primary key.

8. Delete Data
DELETE FROM users WHERE user_id = <some-uuid>;
Use: Remove rows by primary key.

9. Add Column
ALTER TABLE users ADD age int;
Use: Add a new column to an existing table.

10. Drop Table
DROP TABLE users;
Use: Remove a table and its data.

11. Primary Key & Clustering
CREATE TABLE orders (
  order_id UUID,
  customer_id UUID,
  order_date timestamp,
  status text,
  PRIMARY KEY (customer_id, order_id)
) WITH CLUSTERING ORDER BY (order_id DESC);
Use: Define partition key (customer_id) and clustering column (order_id) with sort order.

12. TTL (Time To Live)
INSERT INTO users (user_id, first_name) VALUES (uuid(), 'Alice') USING TTL 86400;
Use: Set expiration (in seconds) for data.

13. Batch Statements
BEGIN BATCH
  INSERT INTO users (user_id, first_name) VALUES (uuid(), 'Alice');
  INSERT INTO users (user_id, first_name) VALUES (uuid(), 'Bob');
APPLY BATCH;
Use: Execute multiple queries atomically.

14. Create Index
CREATE INDEX ON users (last_name);
Use: Create secondary index on a non-primary key column.

15. Describe Keyspace and Tables
DESCRIBE KEYSPACE my_keyspace;
DESCRIBE TABLE users;
Use: Show keyspace/table structure.

16. Data Modeling Tips
Choose partition key carefully for even data distribution.
Use clustering columns to sort data within partitions.
Avoid queries without primary key filtering.
Use denormalization to optimize read performance.

