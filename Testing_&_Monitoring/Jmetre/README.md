# Apache JMeter – Overview & Basics

## What is Apache JMeter?

Apache JMeter is a popular open-source tool designed for load testing and measuring performance of web applications, services, and various protocols. It simulates heavy loads on servers to analyze overall performance and behavior under stress.

---

## Key Features

- **Load Testing:** Simulate multiple users sending requests concurrently.  
- **Performance Testing:** Measure response times, throughput, and resource usage.  
- **Supports Protocols:** HTTP, HTTPS, FTP, JDBC, SOAP, REST, JMS, and more.  
- **Extensible:** Supports plugins and scripting with Groovy, Beanshell, etc.  
- **Distributed Testing:** Run tests from multiple machines for large-scale load.  
- **Reporting:** Generates detailed and customizable test reports and graphs.

---

## How JMeter Works

1. Create a **Test Plan** defining the workflow of requests and assertions.  
2. Add **Thread Groups** to simulate users with configurable load parameters.  
3. Add **Samplers** to specify requests (HTTP, JDBC, etc.).  
4. Add **Listeners** to view and analyze test results.  
5. Run the test and monitor metrics like response time, errors, throughput.

---

## Basic Steps to Use JMeter

### 1. Download and Install

- Download JMeter from [https://jmeter.apache.org/download_jmeter.cgi](https://jmeter.apache.org/download_jmeter.cgi)  
- Unzip and launch `bin/jmeter` (Linux/Mac) or `bin/jmeter.bat` (Windows)

### 2. Create Test Plan

- Open JMeter GUI.  
- Right-click **Test Plan** → Add → Threads (Users) → Thread Group.  
- Configure number of users, ramp-up time, loop count.

### 3. Add Sampler (HTTP Request Example)

- Right-click Thread Group → Add → Sampler → HTTP Request.  
- Enter Server Name/IP, Path, Method, etc.

### 4. Add Listener (View Results)

- Right-click Thread Group → Add → Listener → View Results Tree or Summary Report.

### 5. Run Test

- Click the green **Start** button.  
- Observe results in listeners.

---

## Command Line Mode

Run tests without GUI for better performance:
jmeter -n -t testplan.jmx -l results.jtl -e -o /path/to/report-folder
-n: Non-GUI mode
-t: Test plan file
-l: Log file for results
-e: Generate report dashboard
-o: Output folder for report
