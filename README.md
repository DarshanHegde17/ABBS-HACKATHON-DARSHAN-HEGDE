# ABBS-HACKATHON-DARSHAN-HEGDE


# 🏢 Company & College Review Platform

A web-based platform that allows employees to share role-specific reviews about companies they have worked with. This helps job seekers make informed career decisions based on real employee experiences.

---

## 🚀 Features

### 👨‍💼 Employee Features
- Register and login securely
- Submit company reviews based on job role
- Give overall rating (1–5 stars)
- Add detailed feedback (Pros, Cons, Suggestions)
- Edit and delete own reviews
- Add previous company with proof document upload
- Track review history from dashboard

### 👨‍🎓 Job Seeker Features
- Browse companies
- View reviews role-wise
- Filter reviews by rating and job role
- Search companies

### 👑 Admin Features
- View pending previous company submissions
- Approve or reject employee verification requests
- Manage platform moderation

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|----------|
| Python     | Backend Logic |
| Flask      | Web Framework |
| MongoDB    | Database |
| HTML/CSS   | Frontend UI |
| JavaScript | Client-side interactions |
| Jinja2     | Template Rendering |
| Werkzeug   | Password Hashing |

---

## 📂 Project Structure


project/
│
├── app.py # Main Flask application
├── database.py # MongoDB connection & operations
├── config.py # Configuration settings
│
├── templates/ # HTML templates
│ ├── login.html
│ ├── register.html
│ ├── employee_dashboard.html
│ ├── user_dashboard.html
│ └── admin.html
│
├── static/
│ ├── css/
│ ├── js/
│ └── uploads/ # Uploaded proof documents
│
└── requirements.txt




---

## 🔐 Authentication & Security

- Passwords hashed using `generate_password_hash`
- Session-based authentication
- Role-based access control:
  - `employee_required`
  - `admin_required`
- File upload validation
- Ownership validation for review edits/deletes

---

## 📊 Database Collections

