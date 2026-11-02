# Facial Attendance with Blockchain Records

A Django attendance system that recognises faces with OpenCV and `face_recognition`, and records each recognised check-in in a SHA-256 hash-linked CSV log, alongside student/teacher management, marks, timetables, and dashboards.

## What it does

- **Face-recognition attendance:** loads reference photos from `info/ImagesAttendance/`, encodes them with `face_recognition`, captures webcam frames with OpenCV, and matches faces in real time in the `Attendancee` view.
- **Hash-linked attendance log:** each new check-in appends one row to `info/Attendance.csv` with Name, Time, Date, Block ID, Previous Hash, and Block Hash. The block hash is SHA-256 of the name, time, date, and block ID; the previous row's block hash is stored in the Previous Hash column.
- **Django attendance management:** departments, courses, classes, students, teachers, assignments, timetables, class attendance, attendance totals, and marks, with a custom user model (`info.User`).
- **Dashboards and reports:** attendance views, per-student/course attendance detail, CSV download of the attendance log, and Chart.js-based dashboard pages in the templates.
- **Admin and extras:** Django admin (with django-jazzmin), feedback/contact and to-do views in the `info` app, and the existing test file `info/tests.py`.

## How the face-recognition flow works

1. Add one reference photo per person to `info/ImagesAttendance/`, named after the person (for example `Ali.jpg`).
2. Start the face-attendance view. It builds an encoding for each reference photo.
3. The webcam loop compares each detected face with the known encodings and, on a match, draws the name on the frame and calls `markAttendance`.
4. `markAttendance` adds the person once per CSV file contents (it skips a name already present in `Attendance.csv`) and appends the hash-linked row described above.

Note: the CSV log is separate from the Django database attendance records (`Attendance`, `AttendanceTotal`). The two are not automatically kept in sync.

## Tech stack

- Python, Django, and SQLite (development database)
- OpenCV (`opencv-python`) and `face_recognition`
- NumPy, Pandas, and Matplotlib
- HTML templates with Bootstrap (SB Admin theme) and Chart.js
- django-jazzmin for the admin interface

## Project structure

```text
manage.py               Django entry point
AASystem/               Project settings, URLs, and WSGI config
info/                   Main app: models, views, URLs, admin, templates, static files
info/ImagesAttendance/  Reference face photos (add your own; do not commit real photos)
info/Attendance.csv     Hash-linked attendance log created/updated by the face view
requirements.txt        Python dependencies (unpinned)
README.md               This file
```

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/nasirabbas827/facial-attendance-blockchain.git
cd facial-attendance-blockchain
```

### 2. Create a virtual environment and install dependencies

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

`requirements.txt` lists asgiref, Django, pytz, sqlparse, matplotlib, django-jazzmin, face_recognition, pandas, and opencv-python, without pinned versions. Installing `face_recognition` (and its dlib dependency) can need system build tools; verify the install in your own environment before running the webcam view.

### 3. Apply migrations and create an admin user

```bash
python manage.py migrate
python manage.py createsuperuser
```

### 4. Run the app

```bash
python manage.py runserver
```

Then open http://127.0.0.1:8000/ in your browser. The face-attendance view needs a webcam and reference photos in `info/ImagesAttendance/`.

## Notes and limitations

- The existing README's claims about PostgreSQL/MySQL, deployment, and a "private blockchain" are not stated in the code checked here, so they are not repeated as facts. The database in `AASystem/settings.py` is SQLite, and the hash-linked log is a CSV file, not a distributed blockchain with consensus.
- `AASystem/settings.py` has `DEBUG = True` and `ALLOWED_HOSTS = ['*']`, and a placeholder secret key. Change the secret key, turn debug off, and restrict allowed hosts before any shared or public deployment, and load secrets from environment variables.
- Do not commit real face photos, student CNIC/phone data, or other personal data to a public repository. The student model includes fields such as CNIC and phone number; treat any real data accordingly.
- A stray file, `info/tests.py___jb_tmp___`, is present in the repository; it is not part of the app code checked here.

## Author

Nasir Abbas — Software Developer (Python, Django & Flask, Machine Learning & Blockchain)

GitHub: https://github.com/nasirabbas827
