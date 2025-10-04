
# Megasoft Training Management System (TMS)

## Overview
Megasoft TMS is a **desktop application** designed to streamline the administrative tasks of educational and training centers.  
It provides tools for managing students, courses, and scores efficiently while integrating reporting and data visualization capabilities.

---

## 📘 Features
- **Secure Login** system for authorized access  
- **Student Management**: Add, edit, delete, and view student records  
- **Course Management**: Manage courses, instructors, and durations  
- **Score Management**: Record and update student scores  
- **Reporting & Exporting**: Generate and export PDF reports using iTextSharp  
- **Dynamic Data Lookup** via Countries API  
- **Dashboard Integration** with Power BI for analytics

---

## 🧩 System Architecture
The system follows a **3-Tier Architecture**:

```
+---------------------------+       +----------------------------+       +---------------------+
|   Presentation Layer (UI) | <---> | Business & Data Access Layer| <---> |  Data Layer         |
|      (Windows Forms)      |       |      (C# Logic Classes)    |       |  (SQL Server DB)    |
+---------------------------+       +----------------------------+       +---------------------+
```

### Layers
1. **Presentation Layer (UI):** Windows Forms (.cs) – user interaction  
2. **Business & Data Access Layer:** C# classes managing logic and database connections  
3. **Data Layer:** Microsoft SQL Server database (`megasoft`)

---

## 🛠️ Technology Stack
| Component | Technology |
|------------|-------------|
| Language | C# |
| Framework | .NET Framework 4.7.2 |
| UI | Windows Forms (WinForms) |
| Database | Microsoft SQL Server |
| Libraries | iTextSharp, DGVPrinter, Newtonsoft.Json |

---

## ⚙️ Installation & Setup

### Prerequisites
- Windows OS (7, 8, 10, or 11)
- Visual Studio 2017+
- .NET Framework 4.7.2
- SQL Server + SSMS

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
- `Program.cs` – entry point  
- `DB_connection.cs` – handles database connections  
- `StudentClass.cs`, `CourseClass.cs`, `ScoreClass.cs` – CRUD operations  
- `LoginForm.cs`, `Register_std_Form.cs` – user forms  

---

## 🧱 Database Schema

**Tables:**
- `Users(id, username, password)`  
- `Students(id, first_name, last_name, dob, gender, country, city, ...)`
- `Courses(id, course_name, description, instructor_name, hours)`  
- `Scores(id, student_id, course_id, score, status)`  

All foreign keys use `ON DELETE CASCADE` for data integrity.

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
| Database connection failed | Check SQL Server instance name & connection string |
| API not loading | Verify internet connection |
| Black UI artifacts | Ensure `TransparencyKey` is not set to black in forms |

---

## 📄 License
© 2025 Kyrellos Saleeb. All rights reserved.
