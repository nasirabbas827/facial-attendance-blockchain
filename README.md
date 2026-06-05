# facial_attendance_blockchain  

A web‑based **Facial Attendance System** that records student/teacher check‑ins on a private blockchain for tamper‑proof auditability. The front‑end is built with HTML/CSS (Bootstrap) and the back‑end runs on Django.

---

## Overview  

The application captures a face image, matches it against stored profiles, and logs the attendance event as an immutable transaction on a lightweight blockchain. Administrators can view, export, and analyse attendance data through a responsive dashboard.

---

## Features  

| ✅ | Feature |
|---|---|
| 📸 | **Real‑time facial recognition** using OpenCV / dlib (backend) |
| ⛓️ | **Blockchain‑backed logging** – each attendance entry is stored as a signed block |
| 👤 | **Student & Teacher profiles** with optional photo upload |
| 📊 | **Dashboard** with charts (area, bar, pie) powered by Chart.js |
| 📥 | **CSV export** of attendance records |
| 🔐 | **Admin panel** (Django admin) for managing users and blockchain settings |
| 📱 | **Responsive UI** built on the SB‑Admin Bootstrap theme |

---

## Tech Stack  

| Layer | Technology |
|-------|------------|
| **Front‑end** | HTML5, CSS3, Bootstrap 4 (SB‑Admin), Chart.js |
| **Back‑end** | Python 3.11, Django 5.x |
| **Computer Vision** | OpenCV, dlib (or face‑recognition library) |
| **Blockchain** | Custom lightweight chain (Python objects, SHA‑256 hashing) |
| **Database** | SQLite (development) – can be swapped for PostgreSQL/MySQL |
| **Version Control** | Git (GitHub) |
| **Deployment** | Any WSGI‑compatible server (Gunicorn, uWSGI) |

---

## Installation  

> **Prerequisites**  
> - Python 3.11+  
> - Git  
> - (Optional) virtual‑environment tool (`venv` or `conda`)  

```bash
# 1️⃣ Clone the repo
git clone https://github.com/yourusername/facial_attendance_blockchain.git
cd facial_attendance_blockchain

# 2️⃣ Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate

# 3️⃣ Install Python dependencies
pip install -r requirements.txt   # (Create this file if missing)

# 4️⃣ Apply database migrations
python manage.py migrate

# 5️⃣ Create a superuser for the admin panel
python manage.py createsuperuser
```

> **Note**: If `requirements.txt` is not present, install the core packages manually:

```bash
pip install Django==5.0 opencv-python dlib numpy
```

---

## Usage  

```bash
# Start the development server
python manage.py runserver
```

1. Open `http://127.0.0.1:8000/` in a browser.  
2. Log in with the superuser credentials you created.  
3. Navigate to **Attendance** → **Register** to capture a face image.  
4. The system will match the face, create a new block, and display the entry in the dashboard.  
5. Use the **Export CSV** button to download the