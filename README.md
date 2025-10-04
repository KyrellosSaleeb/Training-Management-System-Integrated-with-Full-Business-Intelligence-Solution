
# Megasoft Training Management System (TMS)

## Overview
Megasoft TMS is a **desktop application** designed to streamline the administrative tasks of educational and training centers.  
It provides tools for managing students, courses, and scores efficiently while integrating reporting, analytics, and a **full data engineering pipeline** powered by SSIS, SSAS, and Power BI.

---

## 📘 Features
- **Secure Login** system for authorized access  
- **Student Management**: Add, edit, delete, and view student records  
- **Course Management**: Manage courses, instructors, and durations  
- **Score Management**: Record and update student scores  
- **Reporting & Exporting**: Generate and export PDF reports using iTextSharp  
- **Dynamic Data Lookup** via Countries API  
- **Dashboard Integration** with Power BI for analytics  
- **End-to-End Data Engineering Pipeline** using SSIS, SSAS, and Power BI for insights

---

## 🧩 System Architecture
The system follows a **3-Tier Architecture**, extended with a **Data Engineering Layer** for analytics and reporting.

```
+---------------------------+       +----------------------------+       +---------------------+
|   Presentation Layer (UI) | <---> | Business & Data Access Layer| <---> |  Data Layer         |
|      (Windows Forms)      |       |      (C# Logic Classes)    |       |  (SQL Server DB)    |
+---------------------------+       +----------------------------+       +---------------------+
                                          |
                                          v
                                  +-------------------+
                                  | Data Engineering  |
                                  | (SSIS, SSAS, PBI) |
                                  +-------------------+
```

### Layers
1. **Presentation Layer (UI):** Windows Forms (.cs) – user interaction  
2. **Business & Data Access Layer:** C# classes managing logic and database connections  
3. **Data Layer:** Microsoft SQL Server database (`megasoft`)  
4. **Data Engineering Layer:** ETL, analytics, and BI integration using SSIS, SSAS, and Power BI

---

## ⚙️ Full Stack Data Engineering Pipeline — *From Raw Data to Insights*

### 🔹 SSIS – Data Ingestion & ETL
Used **SQL Server Integration Services (SSIS)** to automate data extraction, transformation, and loading.  
Created **three databases** to manage data flow:

| Database | Purpose |
|-----------|----------|
| **ODS (Operational Data Store)** | Raw transactional data from Megasoft TMS |
| **STG (Staging)** | Cleaned and validated intermediate data |
| **DWH (Data Warehouse)** | Structured data stored in a **Star Schema** for analytics |

**ETL Process Highlights:**
- Designed **3 SSIS packages** to handle data movement and transformation  
- Implemented **error handling**, **logging**, and **incremental loads**  
- Automated scheduling via **SQL Agent Jobs**

---

### 🔹 SSAS – Analytical Data Model
Developed an **SSAS Tabular Model** to enhance performance and provide advanced analytics.

**Model Features:**
- Star schema design with **fact** and **dimension tables**  
- Created **key measures** for KPIs (total students, pass rates, averages)  
- Applied **DAX formulas** for optimized calculations  
- Deployed as a **tabular model** for direct Power BI connection

---

### 🔹 Power BI – Data Visualization & Insights
Connected **Power BI** to the SSAS Tabular Model (Live Connection).  
Developed a **rich interactive dashboard** for insights and decision-making.

**Dashboard Includes:**
- Student performance analytics  
- Course enrollment and instructor activity  
- Pass/fail distributions and averages by course  
- Dynamic filters by gender, course, role, and location  
- Automated refresh and data-driven visual storytelling

---

## 🛠️ Technology Stack
| Component | Technology |
|------------|-------------|
| Language | C# |
| Framework | .NET Framework 4.7.2 |
| UI | Windows Forms (WinForms) |
| Database | Microsoft SQL Server |
| Data Engineering | SSIS, SSAS, Power BI |
| Libraries | iTextSharp, DGVPrinter, Newtonsoft.Json |

---

## ⚙️ Installation & Setup

### Prerequisites
- Windows OS (7, 8, 10, or 11)
- Visual Studio 2017+  
- .NET Framework 4.7.2  
- SQL Server (with SSIS & SSAS installed)  
- SQL Server Management Studio (SSMS)  
- Power BI Desktop

### Database Setup
```sql
CREATE DATABASE megasoft;
GO
-- Execute provided table scripts (Users, Students, Courses, Scores)
```

### Configure Connection String
Edit `DB_connection.cs`:
```csharp
conn = new SqlConnection("Data Source=YOUR_SERVER;Initial Catalog=megasoft;Integrated Security=True;");
```

### Run the Application
1. Open `TMS_MegaSoft_Project.sln` in Visual Studio  
2. Restore NuGet packages  
3. Press **F5** to run

---

## 👨‍💻 Developer Guide
- `Program.cs` – Entry point  
- `DB_connection.cs` – Manages database connections  
- `StudentClass.cs`, `CourseClass.cs`, `ScoreClass.cs` – Core logic and CRUD  
- `LoginForm.cs`, `Register_std_Form.cs` – User forms and event handlers  

---

## 🧱 Database Schema

**Tables:**
- `Users(id, username, password)`  
- `Students(id, first_name, last_name, dob, gender, country, city, ...)`
- `Courses(id, course_name, description, instructor_name, hours)`  
- `Scores(id, student_id, course_id, score, status)`  

All foreign keys use **ON DELETE CASCADE** for referential integrity.

---

## 🌐 External APIs & Libraries
| Library | Purpose |
|----------|----------|
| **iTextSharp** | PDF generation |
| **DGVPrinter** | Printing DataGridView contents |
| **Newtonsoft.Json** | JSON parsing |
| **CountriesNow API** | Country & City lookup |

---

## 🧩 Troubleshooting
| Issue | Solution |
|--------|-----------|
| Database connection failed | Verify SQL Server instance name and connection string |
| API not loading | Check internet connection |
| Black UI artifacts | Ensure `TransparencyKey` is not set to black in forms |

---

## 📊 End-to-End Data Flow Summary
```
+------------------+
|  Megasoft TMS UI |
+------------------+
          |
          v
+-------------------+
|  SQL Server (ODS) |
+-------------------+
          |
          v
+-------------------+
| SSIS (ETL - STG)  |
+-------------------+
          |
          v
+-------------------+
| DWH (Star Schema) |
+-------------------+
          |
          v
+-------------------+
| SSAS (Tabular)    |
+-------------------+
          |
          v
+-------------------+
| Power BI Reports  |
+-------------------+
```

---

## 📄 License
© 2025 Kyrellos Saleeb. All rights reserved.
