<h1 align="center">🎓 AI System for Avoiding Proxy Students</h1>

<p align="center">
  <b>Smart face-recognition attendance — no more fake mark-ups.</b><br/>
  A student sits in front of the camera, the system knows who they are in seconds.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/OpenCV-Face%20Recognition-green?style=for-the-badge&logo=opencv" />
  <img src="https://img.shields.io/badge/Platform-Windows-lightgrey?style=for-the-badge&logo=windows" />
</p>

---

## 🤔 What is this?

> **The problem:** In many classrooms, one student pretends to be another — a "proxy" — just to mark their friend as present. Traditional paper or manual attendance cannot detect this.
>
> **The solution:** This system uses the **camera on a computer** to look at a student's face and automatically confirm their identity. It is like a security check at an airport — but for classrooms.

---

## ✨ What can it do?

| Feature | What it means for you |
|---|---|
| 📸 **Register a student** | Take 100 photos of a student's face in seconds. The system learns what they look like. |
| 🧠 **Train the AI model** | Click one button. The system studies all registered faces and creates a "memory". |
| ✅ **Mark attendance automatically** | Open the camera. The system recognises each face and writes their name, date, and time into a record. |
| 🚨 **Catch unknown faces** | If an unregistered person appears, the system **beeps an alarm** and saves a photo of that person. |
| ☁️ **Upload records online** | After the session ends, the attendance sheet is sent to a web server automatically — no manual upload needed. |
| 🔐 **Password protection** | Only authorised staff can add new students or train the AI. |

---

## 🖥️ How does it look?

There are **two separate screens** — one for staff, one for daily scanning:

```
┌─────────────────────────────────────────────────────────────────┐
│  Admin Dashboard  (run by teacher / admin)                      │
│  ┌──────────────────────┐  ┌──────────────────────────────────┐ │
│  │  Today's attendance  │  │  Register New Student            │ │
│  │  ID │ NAME │DATE│TIME│  │  Enter ID ___________________    │ │
│  │  ...│ ...  │ ...│ ...│  │  Enter Name _________________    │ │
│  │                      │  │                                  │ │
│  │  [Take Attendance]   │  │  [Take Images]  [Save Profile]   │ │
│  │  [Quit]              │  │                                  │ │
│  └──────────────────────┘  └──────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  Attendance Scanner  (simplified — just press Scan)             │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Today's scanned attendance                              │   │
│  │  ID │ NAME │ DATE │ TIME                                 │   │
│  │  ...│ ...  │ ...  │ ...                                  │   │
│  │                                                          │   │
│  │  [Scan]                          [Quit]                  │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🗂️ Project Structure

```
AI System for Avoid Proxy Student/
│
├── app/
│   ├── admin_dashboard.py        ← Full admin screen (register + train + attendance)
│   ├── attendance_scanner.py     ← Simple scan-only screen (daily use)
│   │
│   ├── TrainingImage/            ← Faces captured during registration
│   ├── TrainingImageLabel/       ← AI model saved here (Trainner.yml)
│   ├── StudentDetails/           ← Student ID + Name records (CSV)
│   ├── Attendance/               ← Daily attendance logs (CSV, one file per day)
│   ├── UnauthorizedImages/       ← Photos of unknown / proxy faces (alarm triggered)
│   │
│   ├── haarcascade_frontalface_default.xml  ← Face-detection engine (bundled)
│   │
│   ├── run_admin_dashboard.bat   ← Double-click to open Admin screen
│   ├── run_attendance_scanner.bat← Double-click to open Scanner screen
│   └── requirements.txt          ← Python libraries needed
│
├── README.md                     ← You are reading this
└── .gitignore                    ← Files excluded from version control
```

---

## 🚀 How to run (step by step)

> **You only need to do steps 1–3 once.**

### Step 1 — Install Python 3.12
Download from [python.org](https://www.python.org/downloads/) and install. Tick **"Add Python to PATH"** during installation.

### Step 2 — Install required libraries
Open a terminal inside the `app/` folder and run:
```bash
pip install -r requirements.txt
```

### Step 3 — Register students (Admin only)
Double-click **`run_admin_dashboard.bat`**.
1. Enter the student's **ID** and **Name**.
2. Click **Take Images** — ask the student to look at the camera.
3. Click **Save Profile** and enter the password to train the AI.

### Step 4 — Daily attendance
Double-click **`run_attendance_scanner.bat`**.
- Click **Scan**.
- Students walk in front of the camera — attendance is marked automatically.
- When done, press **Q** to stop. The record uploads to the server.

---

## ⚙️ How the AI works (plain English)

```
1. CAMERA  →  sees a face
2. DETECTOR →  draws a box around the face  (Haar Cascade algorithm)
3. RECOGNISER → compares the face to all saved faces  (LBPH algorithm)
4. DECISION:
       confidence < 50  →  "KNOWN student"  → mark attendance ✅
       confidence ≥ 50  →  "UNKNOWN person" → beep alarm 🚨 + save photo
```

The AI does **not** send face data to the internet. Everything is processed locally on the computer.

---

## 🔒 Security Notes

> **Warning:** The file `attendance_scanner.py` contains an FTP server address, username, and password in plain text. Before sharing this code publicly, move those credentials to a separate `.env` file or environment variables.

---

## 📦 Dependencies

| Library | Purpose |
|---|---|
| `opencv-contrib-python` | Face detection and recognition |
| `numpy` | Image data processing |
| `Pillow` | Loading image files |
| `pandas` | Reading and writing CSV records |
| `tkinter` *(built-in)* | Graphical user interface |
| `winsound` *(built-in, Windows)* | Alarm beep for unknown faces |
| `ftplib` *(built-in)* | Uploading attendance to server |

---

## 👨‍💻 Built by

Final Year Project — *AI System for Avoiding Proxy Students*  
Developed using Python, OpenCV, and Tkinter on Windows.

---

<p align="center">Made with ❤️ to make classrooms more honest.</p>
