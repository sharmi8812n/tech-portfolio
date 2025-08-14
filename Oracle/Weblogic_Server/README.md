# ☁️ Oracle WebLogic Server

## Overview

**Oracle WebLogic Server** is a Java EE application server used for building and deploying enterprise Java applications. It supports web applications, EJBs, JMS, web services, and more in a highly scalable and reliable environment.

---

## 🚀 Features

- ✅ Java EE (Jakarta EE) compliant
- ☁️ Cloud-ready (Docker, Kubernetes, OCI)
- ♻️ High Availability & Clustering
- 🔐 Integrated security framework (JAAS, LDAP, SAML, etc.)
- 📈 Administration via Web Console, WLST (scripting), REST APIs

---

## 🛠️ Installation

### 1. Prerequisites

- Java Development Kit (JDK) 8 or 11
- Oracle WebLogic Installer (download from Oracle site)

### 2. Install WebLogic

# Set JAVA_HOME
export JAVA_HOME=/path/to/jdk

# Run installer
java -jar fmw_12.2.1.x.x_wls.jar

---
### Step-by-Step Deployment Guide
1. Prepare your JAR
Make sure the JAR is a deployable module (EJB JAR, utility JAR, etc.).
If it’s part of a larger app, package it inside an EAR.

2. Access WebLogic Admin Console
Open browser and navigate to:
http://<admin-server-host>:<admin-server-port>/console
Login with Admin credentials.

4. Deploy via Admin Console
Go to Deployments from the Domain Structure panel.
Click Install.
Browse and select your JAR file.
Click Next.

4. Target the Managed Server
Select the Managed Server (e.g., ManagedServer1) as the deployment target.
Click Next.

5. Configure deployment options
Choose Install this deployment as an application or module.
Complete any additional configuration as needed.
Click Finish to deploy.

6. Start/Activate Deployment
If the deployment is not automatically started, select it from the Deployments list.
Click Start → Servicing all requests.

7. Verify deployment
Check Status column in Deployments — it should show Active.
Review Managed Server logs for any errors.
