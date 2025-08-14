# Apache Kafka – Overview & Quickstart Guide

## 📌 What is Apache Kafka?

Apache Kafka is a distributed event streaming platform capable of handling trillions of events a day. It is used to build real-time data pipelines and streaming applications that are fast, scalable, and durable.

---

## 🧠 Key Concepts

| Term          | Description |
|---------------|-------------|
| **Producer**  | Sends messages (events) to Kafka topics |
| **Consumer**  | Reads messages from Kafka topics |
| **Topic**     | Logical channel for message streams |
| **Partition** | Splits topic into multiple logs for parallelism |
| **Broker**    | Kafka server that handles data streams |
| **Zookeeper** | (Legacy) Manages Kafka metadata and configurations |

---

## 🏗 Kafka Architecture

    Producer → Kafka Topic (Partitioned) → Consumer →  Kafka Broker (Cluster)→ Zookeeper (optional)

---

## 🚀 Getting Started (Local Setup)

### ✅ Prerequisites

- Java 8+
- Kafka binaries: https://kafka.apache.org/downloads

### 📁 Step-by-Step Setup

# Start Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Start Kafka Broker
bin/kafka-server-start.sh config/server.properties

# Create a Topic
bin/kafka-topics.sh --create \
  --topic my-topic \
  --bootstrap-server localhost:9092 \
  --partitions 1 \
  --replication-factor 1
  
# List Topics
bin/kafka-topics.sh --list --bootstrap-server localhost:9092

# 📨 Start a Producer (send messages)
bin/kafka-console-producer.sh \
  --topic my-topic \
  --bootstrap-server localhost:9092
Then type some messages and hit Enter.

# 📥 Start a Consumer (receive messages)
bin/kafka-console-consumer.sh \
  --topic my-topic \
  --from-beginning \
  --bootstrap-server localhost:9092

## 🛠 Useful Commands
#  🔍 Describe Topic
bin/kafka-topics.sh --describe --topic my-topic --bootstrap-server localhost:9092

#  ❌ Delete Topic
bin/kafka-topics.sh --delete --topic my-topic --bootstrap-server localhost:9092

#  🧪 Send Key/Value Pairs
    bin/kafka-console-producer.sh \
      --topic my-topic \
      --bootstrap-server localhost:9092 \
      --property "parse.key=true" \
      --property "key.separator=:"
    Then enter:
    user1:message for user 1
    user2:message for user 2

# 📦 Example Use Case: Logging Service
    Producer: App logs events and sends to topic app-logs.
    Kafka Broker: Holds and replicates logs in partitions.
    Consumer: Log analytics service processes logs in real-time.

✅ Summary

Kafka is ideal for real-time data streaming and decoupling microservices with reliable message delivery. It supports scalable, fault-tolerant, and persistent messaging — a core component of modern data architecture.
