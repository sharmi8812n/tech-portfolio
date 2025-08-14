# 📊 Power BI – Business Intelligence & Data Visualization

## Overview

**Power BI** is a Microsoft business analytics platform that allows users to visualize data, share insights, and create interactive dashboards and reports from multiple data sources. It supports both cloud-based and on-premise data and integrates tightly with Microsoft tools like Excel, Azure, SQL Server, and more.

---

## ✅ Features

- 📈 Drag-and-drop report building
- 🔌 Data connectors (Excel, SQL, Azure, REST APIs, etc.)
- 🧮 DAX (Data Analysis Expressions) for advanced calculations
- 💡 AI-powered insights
- 🔐 Row-Level Security (RLS)
- 🌐 Web and mobile sharing via Power BI Service

---

## 🛠️ Installation

### Power BI Desktop (Windows)

Download: [https://powerbi.microsoft.com/desktop](https://powerbi.microsoft.com/desktop)

> Note: Power BI Desktop is Windows-only. Mac users can use Power BI via browser or run a Windows VM.

---

## 🔗 Connect to Data Sources

### Common Connectors

| Source       | Connector                          |
|--------------|-------------------------------------|
| Excel        | Excel Workbook                     |
| SQL Server   | SQL Server Database                |
| Web API      | Web → REST API endpoint            |
| SharePoint   | SharePoint Folder/List             |
| Azure        | Azure SQL, Azure Blob, etc.        |

1. Click **Home → Get Data**
2. Choose a data source
3. Enter connection details
4. Load or transform data via Power Query

---

## 🧮 Data Modeling

- Create relationships between tables (1:1, 1:N, M:N)
- Add calculated columns or measures using **DAX**

### Example DAX Measure

DAX
Total Sales = SUM(Sales[Amount])
---

## 🎨 Create Visualizations
Use visuals like Bar, Line, Map, Pie, Table, KPI, etc.
Customize formatting (colors, labels, filters)
Use slicers for interactivity

## 🔄 Refresh & Schedule
Manual refresh via Power BI Desktop
Publish to Power BI Service to schedule refreshes
Supported for cloud & on-prem connectors via Gateway

## ☁️ Power BI Service (cloud)
Sign in: https://app.powerbi.com
Upload .pbix files from Desktop
Create dashboards by pinning visual tiles
Share reports with users or groups

## 👥 Sharing & Collaboration
Share with individuals or Microsoft 365 groups
Publish to web (public view, limited use)
Embed reports in apps (PowerApps, Dynamics, custom web apps)
Export reports to PDF or PowerPoint

## 🔐 Security
Row-Level Security (RLS): Restrict data access by user
Use Azure AD for authentication & access control
Audit logs and usage metrics available via Admin portal

## 🧪 Power BI in CI/CD & DevOps
Store .pbix files in Git repositories
Use Power BI REST API or Power BI CLI to automate deployment
Tools: Azure DevOps, PowerShell, pbi-tools

## 🧰 Tools & Extensions
Power BI CLI: npm install -g powerbi-cli
Tabular Editor: Manage data models outside of Power BI
DAX Studio: Advanced DAX development and diagnostics
Power BI Report Builder: For paginated reports (SSRS-style)
