# Student Management System (SMS)

## Overview

The Student Management System (SMS) is a full-stack web application built with Django that centralizes student, faculty, attendance, course, and academic records management.

The goal is to provide a scalable, maintainable, and secure platform that can be extended into a complete college ERP solution.

---

# Project Goals

1. Centralized student data management.
2. Role-based access for Admins, Faculty, and Students.
3. Automated attendance tracking.
4. Academic performance monitoring.
5. Dashboard-driven reporting.
6. Modular architecture for future expansion.

---

# Technology Stack

## Backend

* Python 3.12+
* Django 5.x
* Django ORM
* Django Authentication System

## Frontend

* HTML5
* CSS3
* Bootstrap 5
* JavaScript

## Database

Development:

* SQLite

Production:

* PostgreSQL

## Deployment

* Gunicorn
* Nginx
* Ubuntu Server

---

# System Architecture

```text
Browser
   │
   ▼
Django URLs
   │
   ▼
Views
   │
   ▼
Services / Business Logic
   │
   ▼
Models (ORM)
   │
   ▼
Database
```

Request Flow:

1. User sends request.
2. URL routes request.
3. View validates request.
4. Business logic executes.
5. ORM communicates with database.
6. Response returned as HTML or JSON.

---

# User Roles

## Administrator

Responsibilities:

* Manage students
* Manage faculty
* Manage courses
* View reports
* Configure system

Permissions:

CRUD on all modules.

---

## Faculty

Responsibilities:

* Mark attendance
* Upload marks
* View assigned students

Permissions:

Limited to assigned courses and students.

---

## Student

Responsibilities:

* View profile
* View attendance
* View marks

Permissions:

Read-only access to personal records.

---

# Application Modules

---

## 1. Authentication Module

### Purpose

Handle user login and authorization.

### Django Apps

```text
accounts/
```

### Features

* Login
* Logout
* Password reset
* User creation
* Role assignment

### Models

```python
class User(AbstractUser):
    role = models.CharField(max_length=20)
```

### Tasks

Backend:

* Custom User model
* Authentication Views
* Permission Decorators

Frontend:

* Login Page
* Registration Page

---

## 2. Student Module

### Purpose

Store and manage student information.

### Django App

```text
students/
```

### Features

* Add Student
* Edit Student
* Delete Student
* Search Student
* Student Profile

### Model

```python
class Student(models.Model):
    user = models.OneToOneField(User)
    roll_no = models.CharField(max_length=20)
    department = models.CharField(max_length=100)
    year = models.IntegerField()
    phone = models.CharField(max_length=15)
```

### APIs

```text
GET    /students/
GET    /students/<id>/
POST   /students/create/
PUT    /students/update/
DELETE /students/delete/
```

### Assigned Contributor

Student Management Team

---

## 3. Faculty Module

### Purpose

Maintain faculty records.

### Django App

```text
faculty/
```

### Features

* Faculty Registration
* Faculty Assignment
* Faculty Profile

### Model

```python
class Faculty(models.Model):
    user = models.OneToOneField(User)
    department = models.CharField(max_length=100)
    designation = models.CharField(max_length=100)
```

### APIs

```text
GET /faculty/
POST /faculty/create/
PUT /faculty/update/
```

### Assigned Contributor

Faculty Management Team

---

## 4. Course Module

### Purpose

Store subject information.

### Django App

```text
courses/
```

### Features

* Add Course
* Update Course
* Assign Faculty
* Assign Students

### Model

```python
class Course(models.Model):
    name = models.CharField(max_length=100)
    code = models.CharField(max_length=20)
    faculty = models.ForeignKey(Faculty)
```

### APIs

```text
GET /courses/
POST /courses/create/
PUT /courses/update/
```

### Assigned Contributor

Course Team

---

## 5. Attendance Module

### Purpose

Track daily attendance.

### Django App

```text
attendance/
```

### Features

* Mark Attendance
* Attendance Reports
* Percentage Calculation

### Model

```python
class Attendance(models.Model):
    student = models.ForeignKey(Student)
    course = models.ForeignKey(Course)
    date = models.DateField()
    status = models.BooleanField()
```

### Attendance Formula

```text
Attendance % =
(Present Classes / Total Classes) × 100
```

### APIs

```text
POST /attendance/mark/
GET  /attendance/report/
```

### Assigned Contributor

Attendance Team

---

## 6. Marks Module

### Purpose

Store academic scores.

### Django App

```text
marks/
```

### Features

* Add Marks
* Edit Marks
* Grade Calculation
* Semester Results

### Model

```python
class Marks(models.Model):
    student = models.ForeignKey(Student)
    course = models.ForeignKey(Course)
    marks = models.IntegerField()
```

### Grade Logic

```text
90 - 100  => A+
80 - 89   => A
70 - 79   => B
60 - 69   => C
<60       => F
```

### APIs

```text
POST /marks/add/
GET  /marks/report/
```

### Assigned Contributor

Academic Team

---

## 7. Dashboard Module

### Purpose

Display analytics and summaries.

### Django App

```text
dashboard/
```

### Admin Dashboard

Widgets:

* Total Students
* Total Faculty
* Total Courses
* Attendance Overview

### Faculty Dashboard

Widgets:

* Assigned Subjects
* Today's Attendance

### Student Dashboard

Widgets:

* Attendance %
* Recent Marks
* GPA

### Assigned Contributor

Dashboard Team

---

# Database Relationships

```text
User
 │
 ├── Student
 │
 └── Faculty

Faculty
 │
 └── Course

Student
 │
 ├── Attendance
 │
 └── Marks

Course
 │
 ├── Attendance
 │
 └── Marks
```

---

# Folder Structure

```text
student_management/

├── manage.py

├── accounts/
├── students/
├── faculty/
├── courses/
├── attendance/
├── marks/
├── dashboard/

├── templates/
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── media/
│
├── requirements.txt
│
└── student_management/
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

---

# Coding Standards

## Naming

Models:

```python
Student
Faculty
Attendance
```

Variables:

```python
student_name
faculty_id
attendance_count
```

Functions:

```python
calculate_attendance()
create_student()
generate_report()
```

---

# Git Workflow

Main Branch:

```text
main
```

Development Branch:

```text
develop
```

Feature Branches:

```text
feature/authentication
feature/student-module
feature/attendance-module
feature/dashboard
```

Workflow:

1. Create feature branch.
2. Commit changes.
3. Push branch.
4. Open Pull Request.
5. Code Review.
6. Merge into develop.
7. Release into main.

---

# Future Enhancements

Phase 2:

* Fee Management
* Parent Portal
* Notifications

Phase 3:

* REST API
* Mobile App
* AI Performance Prediction
* Timetable Generator

---

# Deliverables

Each contributor must provide:

1. Models
2. URLs
3. Views
4. Templates
5. Forms
6. Unit Tests
7. Documentation

No module is considered complete until all seven components are implemented and reviewed.
