# CGPA Planner Pro — JUET CSE 🎓

A feature-rich, dark-themed academic planner built specifically for **B.Tech CSE students at Jaypee University of Engineering and Technology (JUET), Guna**. Track your SGPA semester by semester, calculate your live CGPA, simulate future outcomes, and store everything securely in the cloud with real Firebase authentication.

---

## ✨ Features

### 🔐 Real User Authentication (Firebase)
- Create an account with name, email, enrollment number and password
- Secure sign-in / sign-out powered by **Firebase Authentication**
- Forgot password — sends a real reset link to your email
- Change password and delete account from within the app

### 💾 Cloud Database (Firestore)
- All grade data is saved to **Google Firestore** in real time
- Auto-saves 2.5 seconds after any change
- Data loads back instantly on next login — from any device, any browser
- Each user's data is fully isolated (only you can see your data)
- Activity log tracks your last 10 saves, exports and account changes

### 📝 Two Grade Entry Modes
| Mode | How it works |
|---|---|
| **Quick SGPA** | Type one SGPA per semester directly — fastest way to enter data |
| **Subject-wise** | Enter individual subject credits + grade (O/A+/A/B+/B/C/P/F) — SGPA auto-calculated live |

### 📊 Analysis & Charts
- **SGPA Trend** — line chart showing your performance across all semesters
- **CGPA Trajectory** — running CGPA with optional target line overlay
- **Credits Progress** — cumulative credits earned vs total 160
- **Semester Breakdown** — color-coded bar chart (cyan = O, green = A, amber = B+, red = below)
- **Insights panel** — avg SGPA, range, trend direction (improving/declining/stable), equivalent %

### 🎯 Target CGPA Planner
- Set a target CGPA and instantly see:
  - Average SGPA needed across all remaining semesters
  - Exact SGPA needed in the next semester
  - Maximum CGPA still achievable
  - Whether target is achievable, needs effort, or is no longer possible
  - Progress bar showing how far along you are
  - Per-semester suggested SGPA strategy

### 🔮 What-If Scenario Planner
- Simulate any semester's SGPA without affecting real data
- Add multiple scenarios and see the **projected CGPA** and **percentage change** live
- Auto-fill all remaining semesters with one click

### 📄 PDF Export
- Export a professional dark-themed report with:
  - Your name and enrollment number in the header
  - CGPA, max achievable, division summary boxes
  - Full semester-wise performance table with grade points and percentages
  - Target analysis section (if target is set)

### 📖 Reference Tab
- Complete grade point scale (O to F)
- Division / classification table
- Percentage formula: `Percentage = CGPA × 10`
- Full JUET CSE credit structure — all 8 semesters, all subjects with codes and credits

---

## 🏛 JUET CSE Curriculum (Built-in)

The app uses the **official JUET CSE B.Tech curriculum** with exact subject names, course codes, and credit values as per the university's published course structure.

| Semester | Credits | Key Subjects |
|---|---|---|
| Sem 1 | 19.5 | Engineering Mathematics, Physics-1, English, Computer Programming |
| Sem 2 | 22.5 | Discrete Mathematics, Physics-2, Electrical Science, OOP |
| Sem 3 | 20 | Data Structures, Digital Systems & Microprocessors, Database Systems |
| Sem 4 | 21 | Algorithms, Computer Organisation & Architecture, Machine Learning |
| Sem 5 | 26 | Probability Theory, Computer Networks, Theory of Computation, Minor Project-1 |
| Sem 6 | 18 | Operating Systems, Compiler Design, Minor Project-2 |
| Sem 7 | 16 | CS Electives (×4), Major Project Part-I |
| Sem 8 | 17 | CS Electives (×2), Open Elective, Major Project Part-II |
| **Total** | **160** | *(Audit/Value Added courses excluded from CGPA as per university rules)* |

---

## 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| **HTML / CSS / JavaScript** | Single-file frontend, no build tools needed |
| **Firebase Authentication** | Real user accounts and secure login |
| **Cloud Firestore** | Real-time database for storing academic data |
| **Chart.js** | Interactive performance charts |
| **jsPDF** | Client-side PDF report generation |
| **Google Fonts** | Space Mono + DM Sans typography |

> No Node.js, no npm, no build step. The entire app is one `.html` file.

---

## 🚀 Setup & Deployment

### Prerequisites
- A [Firebase](https://console.firebase.google.com) account (free)

### Step 1 — Clone the repository
```bash
git clone https://github.com/your-username/cgpa-planner-pro.git
cd cgpa-planner-pro
```

### Step 2 — Create a Firebase project
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Create a project** → enter a name → disable Analytics → click **Create**

### Step 3 — Enable Authentication
1. In the left sidebar → **Authentication** → **Get started**
2. Under **Sign-in method** → click **Email/Password** → toggle **Enable** → **Save**

### Step 4 — Create Firestore Database
1. Left sidebar → **Firestore Database** → **Create database**
2. Select **Start in test mode** → choose a location (e.g. `asia-south1`) → **Done**

### Step 5 — Get your Firebase config
1. Click the ⚙️ gear icon → **Project settings**
2. Under **Your apps** → click `</>` (Web) → register the app
3. Select **"Use a `<script>` tag"** — copy the `firebaseConfig` object

### Step 6 — Add your config to the file
Open `cgpa_planner.html` and find this section near the bottom:

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT.firebasestorage.app",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

Replace with your own values from the Firebase console.

### Step 7 — Set Firestore Security Rules
In Firebase Console → **Firestore Database** → **Rules** tab, replace the default rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
    match /academics/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

Click **Publish**. This ensures every user can only access their own data.

### Step 8 — Open in browser
```bash
# Just open the file directly — no server needed
open cgpa_planner.html
```

Or deploy to **GitHub Pages**, **Netlify**, **Vercel**, or any static host — it's a single HTML file.

---

## 📁 Project Structure

```
cgpa-planner-pro/
│
├── cgpa_planner.html     # The entire application (single file)
└── README.md             # This file
```

---

## 🌐 Deploying to GitHub Pages

1. Push the repo to GitHub
2. Go to **Settings** → **Pages**
3. Under **Source** → select **main branch** → `/ (root)`
4. Click **Save** — your app will be live at `https://your-username.github.io/cgpa-planner-pro/cgpa_planner.html`

---


## 🔒 Security Notes

- Passwords are **hashed by Firebase** using industry-standard bcrypt — never stored as plain text
- Each user's Firestore documents are **protected by security rules** — only the authenticated owner can read or write their data
- Firebase API keys in the frontend are safe to be public — they identify your project but don't grant admin access
- For production use, restrict your API key in the [Google Cloud Console](https://console.cloud.google.com) to only allow requests from your domain

---

## 🤝 Contributing

Contributions are welcome! If you're a JUET student and notice any subject name, code, or credit mismatch with the latest curriculum, please open an issue or pull request.

```bash
# Fork the repo, make your changes, then open a PR
git checkout -b fix/curriculum-update
git commit -m "Update Sem 5 subject credits"
git push origin fix/curriculum-update
```

---

## 📄 License

MIT License — free to use, modify and distribute.

---

## 👨‍💻 Author

Built with ❤️ by Abhinav, for JUET CSE students.

> *"Your CGPA doesn't define you, but this planner definitely helps it."*

---

## ⭐ Star this repo if it helped you!
