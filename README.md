<div align="center">

<!-- BANNER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=200&section=header&text=University%20DBMS&fontSize=60&fontColor=e94560&fontAlignY=38&desc=Prototype%20Database%20Management%20System&descAlignY=58&descColor=a8b2d8&animation=fadeIn" width="100%"/>

<br/>

<!-- BADGES -->
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge&logo=statuspage)
![Database](https://img.shields.io/badge/Database-SQL-blue?style=for-the-badge&logo=postgresql&logoColor=white)
![Type](https://img.shields.io/badge/Type-Prototype-orange?style=for-the-badge&logo=databricks)
![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge&logo=opensourceinitiative)

<br/>

> **A comprehensive, relational database prototype designed to manage the complete  
> academic and administrative ecosystem of a modern university.**

<br/>

---

</div>

## 📌 Table of Contents

- [📖 Overview](#-overview)
- [✨ Features](#-features)
- [🗂️ Database Schema](#️-database-schema)
- [🔗 Entity Relationships](#-entity-relationships)
- [📋 Module Breakdown](#-module-breakdown)
- [⚙️ Tech Stack](#️-tech-stack)
- [🚀 Getting Started](#-getting-started)
- [📁 Project Structure](#-project-structure)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 📖 Overview

The **University Database Management System (UDBMS)** is a prototype relational database system built to centralize and manage all critical data operations of a university. It handles everything from student enrollment and academic records to employee payroll and course scheduling — all under one unified schema.

This project demonstrates core database design principles including:
- ✅ Entity-Relationship (ER) Modeling
- ✅ Schema Normalization (up to 3NF/BCNF)
- ✅ Referential Integrity & Constraints
- ✅ Complex Query Design (Joins, Subqueries, Views)
- ✅ Stored Procedures & Triggers

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎓 **Student Management** | Store and manage student profiles, enrollment, majors, minors & academic history |
| 👨‍🏫 **Instructor Management** | Track instructor assignments, courses taught, and department affiliations |
| 📚 **Course Catalog** | Maintain courses with prerequisite chains and credit information |
| 🏫 **Section & Scheduling** | Manage class sections, locations, time slots, and semester info |
| 📊 **Grades & Transcripts** | Record student grades per class and generate academic transcripts |
| 💼 **Employee Records** | Store full employee data including roles, departments, and benefits |
| 💰 **Benefits Administration** | Track employee benefit packages and eligibility |
| 🗓️ **Semester Tracking** | Organize all academic activity by semester and academic year |

---

## 🗂️ Database Schema

The system is organized into the following major entity groups:

### 🎓 Academic Domain

```
┌─────────────┐       ┌──────────────┐       ┌─────────────────┐
│   STUDENT   │──────▶│  ENROLLMENT  │◀──────│     SECTION     │
│─────────────│       │──────────────│       │─────────────────│
│ student_id  │       │ student_id   │       │ section_id      │
│ name        │       │ section_id   │       │ course_id       │
│ dob         │       │ semester_id  │       │ instructor_id   │
│ email       │       │ grade        │       │ semester_id     │
│ address     │       └──────────────┘       │ location        │
└─────────────┘                              │ time_slot       │
                                             └─────────────────┘
```

### 📚 Course Domain

```
┌─────────────┐       ┌──────────────────┐
│   COURSE    │──────▶│  PREREQUISITE    │
│─────────────│       │──────────────────│
│ course_id   │       │ course_id        │
│ title       │       │ prereq_id        │
│ credits     │       └──────────────────┘
│ dept_id     │
└─────────────┘
```

### 💼 Employee Domain

```
┌──────────────┐       ┌──────────────────┐
│   EMPLOYEE   │──────▶│    BENEFITS      │
│──────────────│       │──────────────────│
│ employee_id  │       │ benefit_id       │
│ name         │       │ employee_id      │
│ dept_id      │       │ type             │
│ role         │       │ coverage         │
│ salary       │       │ start_date       │
└──────────────┘       └──────────────────┘
```

---

## 🔗 Entity Relationships

```
STUDENT ──< ENROLLMENT >── SECTION ──< TEACHES >── INSTRUCTOR
   |                          |                          |
   |                       COURSE ──< PREREQ >── COURSE |
   |                          |                          |
MAJOR/MINOR               SEMESTER                 DEPARTMENT
   |                                                     |
   └──────────────────────────────────────── EMPLOYEE ──┘
                                                  |
                                               BENEFITS
```

---

## 📋 Module Breakdown

### 1️⃣ Courses & Prerequisites
- Each course may have zero or more prerequisite courses
- Supports multi-level prerequisite chains
- Prevents circular dependencies via constraints

### 2️⃣ Instructors, Courses & Sections
- An instructor can teach multiple sections per semester
- Each section is linked to a specific course and semester
- Supports full-time and adjunct instructor records

### 3️⃣ Students, Classes & Grades
- Students enroll in sections (not just courses)
- Grades stored per enrollment record
- GPA calculation via views or stored procedures

### 4️⃣ Classes, Location & Semester
- Each section has a designated room/building location
- Time-slot management for conflict detection
- Semester table stores start/end dates and academic year

### 5️⃣ Employee Benefits
- Employees can have multiple benefit plans
- Tracks benefit type (health, dental, pension, etc.)
- Effective date and eligibility rules supported

### 6️⃣ Student Majors & Minors
- Students can declare one or more majors and minors
- Linked to department and program tables
- Historical tracking of major changes

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| 🗄️ **Database Engine** | PostgreSQL / MySQL / Oracle (adaptable) |
| 📝 **Query Language** | SQL (DDL + DML + DCL) |
| 🧰 **Design Tools** | ER Diagram Tools (Draw.io / dbdiagram.io) |
| 🔧 **Scripts** | `.sql` files for schema, seed data & queries |
| 📄 **Documentation** | Markdown |

---

## 🚀 Getting Started

### Prerequisites

Make sure you have a relational database engine installed:

```bash
# For PostgreSQL
sudo apt install postgresql postgresql-contrib

# For MySQL
sudo apt install mysql-server
```

### Installation & Setup

```bash
# 1. Clone the repository
git clone https://github.com/your-username/university-dbms.git
cd university-dbms

# 2. Connect to your database
psql -U postgres        # PostgreSQL
mysql -u root -p        # MySQL

# 3. Create the database
CREATE DATABASE university_db;
\c university_db        # PostgreSQL
USE university_db;      # MySQL

# 4. Run the schema script
\i sql/schema.sql       # PostgreSQL
SOURCE sql/schema.sql;  # MySQL

# 5. Load sample data
\i sql/seed_data.sql
SOURCE sql/seed_data.sql;

# 6. Run sample queries
\i sql/queries.sql
SOURCE sql/queries.sql;
```

---

## 📁 Project Structure

```
university-dbms/
│
├── 📂 sql/
│   ├── schema.sql          # All CREATE TABLE statements
│   ├── constraints.sql     # FK, PK, CHECK constraints
│   ├── seed_data.sql       # Sample/test data
│   ├── queries.sql         # Sample SELECT queries
│   ├── views.sql           # Reusable database views
│   └── procedures.sql      # Stored procedures & triggers
│
├── 📂 diagrams/
│   ├── er_diagram.png      # Entity-Relationship Diagram
│   └── schema_diagram.png  # Relational Schema Diagram
│
├── 📂 docs/
│   ├── data_dictionary.md  # Field-by-field documentation
│   └── assumptions.md      # Design decisions & notes
│
└── README.md
```

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. 🍴 **Fork** the repository
2. 🌿 **Create** a new branch: `git checkout -b feature/your-feature`
3. 💾 **Commit** your changes: `git commit -m "Add: your feature description"`
4. 📤 **Push** to the branch: `git push origin feature/your-feature`
5. 🔁 **Open** a Pull Request

Please make sure your SQL follows the existing naming conventions and includes comments.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f3460,50:16213e,100:1a1a2e&height=120&section=footer" width="100%"/>

**Made with ❤️ for academic excellence**

⭐ *If you found this useful, please consider giving it a star!* ⭐

</div>
