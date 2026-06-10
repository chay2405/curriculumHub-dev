# 🎓 CurrHub — GenAI Curriculum Generator

> AI-Powered Educational Curriculum Design Platform for Faculty and Students

![Made with React](https://img.shields.io/badge/Made%20with-React-61DAFB?style=for-the-badge&logo=react)
![Firebase](https://img.shields.io/badge/Firebase-Firestore%20%2B%20Auth-FFCA28?style=for-the-badge&logo=firebase)
![Groq AI](https://img.shields.io/badge/Groq-LLaMA%203.3%2070B-F55036?style=for-the-badge)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?style=for-the-badge&logo=tailwind-css)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

---

## 📋 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [How It Works (Faculty)](#-how-it-works-faculty)
- [How It Works (Student)](#-how-it-works-student)
- [Sage AI Study Companion](#-sage-ai-study-companion)
- [Firebase Structure](#-firebase-structure)
- [Environment Variables](#-environment-variables)
- [Installation & Setup](#-installation--setup)
- [Firebase Setup Guide](#-firebase-setup-guide)
- [Groq API Setup](#-groq-api-setup)
- [Running the Project](#-running-the-project)
- [Deployment](#-deployment)

---

## 🔍 About the Project

CurrHub is a full-stack AI-powered web platform that enables faculty members to generate comprehensive, semester-wise educational curricula using the LLaMA 3.3 70B language model via Groq API. Faculty enter parameters like skill, education level, number of semesters, weekly hours, and industry focus — and the AI generates a complete structured curriculum in seconds.

Designing a curriculum manually is time-consuming, inconsistent, and often misaligned with industry needs. CurrHub solves this by automating curriculum generation with AI, ensuring every course, topic, and learning outcome is relevant, structured, and industry-aligned. Faculty can publish curricula directly to their college's students with one click.

Students from the same college can browse all published curricula, download them as PDF or JSON, and interact with Sage — an AI study companion that generates personalized learning roadmaps. Sage integrates new topics the student wants to learn alongside their existing semester schedule, creating a unified study plan.

---

## ✨ Features

### 👨‍🏫 Faculty Features

| Feature | Description | Where in App |
| :--- | :--- | :--- |
| **AI Curriculum Generation** | Enter skill + parameters → LLaMA 3.3 generates full semester-wise curriculum | Generate Curriculum page |
| **Save as Draft** | Save generated curriculum privately without sharing | Generate Curriculum page |
| **Publish to College** | Instantly share curriculum with all students in same college | Generate Curriculum page |
| **My Curricula** | View, manage, publish, or delete all created curricula | My Curricula page |
| **Generation History** | Full log of every curriculum generation attempt with search and filter | Generation History page |
| **Student Comments** | Read all feedback students leave on published curricula | Comments page |
| **Dashboard Analytics** | Stats — total generated, published, comments received | Dashboard |

### 👩‍🎓 Student Features

| Feature | Description | Where in App |
| :--- | :--- | :--- |
| **Browse Curricula** | View all published curricula from their college | Browse Curricula page |
| **Download PDF** | Export full curriculum as formatted multi-page PDF | Curriculum Detail page |
| **Download JSON** | Export raw curriculum data as JSON file | Curriculum Detail page |
| **Post Comments** | Leave feedback and questions on any curriculum | Curriculum Detail page |
| **Sage AI Companion** | AI chatbot that generates personalized learning roadmaps | Sage AI page |
| **Sage History** | View and continue all past Sage conversations | Sage History page |
| **View History** | Track which curricula have been viewed | View History page |
| **My Comments** | Manage all comments posted | My Comments page |
| **Dashboard Stats** | Overview of available curricula, Sage usage, activity | Dashboard |

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| Frontend | React 18 + Vite | UI framework and build tool |
| Styling | Tailwind CSS | Utility-first CSS framework |
| Routing | React Router v6 | Client-side navigation |
| Authentication | Firebase Auth | Email/Password login and registration |
| Database | Firebase Firestore | Real-time NoSQL cloud database |
| AI Model | Groq API (LLaMA 3.3 70B) | Curriculum generation and Sage AI |
| PDF Export | jsPDF + jspdf-autotable | Client-side PDF generation |
| Notifications | react-hot-toast | Success and error toasts |
| Font | Plus Jakarta Sans | Primary typography |
| Deployment | Vercel | Frontend hosting |

---

## 📁 Project Structure

```
currhub/
├── .env                          # Your local environment variables (never commit)
├── .env.example                  # Template showing required variable names
├── .gitignore                    # Files excluded from git (includes .env)
├── index.html                    # HTML entry point, loads Plus Jakarta Sans font
├── package.json                  # Dependencies and npm scripts
├── vite.config.js                # Vite build configuration
├── tailwind.config.js            # Tailwind CSS configuration
├── postcss.config.js             # PostCSS configuration for Tailwind
├── README.md                     # This file
└── src/
    ├── main.jsx                  # React app entry point, wraps app in providers
    ├── App.jsx                   # Root component, defines all routes
    ├── index.css                 # Tailwind directives + custom animations
    ├── firebase.js               # Firebase app initialization, exports auth + db
    ├── context/
    │   └── AuthContext.jsx       # Global auth state, login/register/logout functions
    ├── hooks/
    │   ├── useAuth.js            # Custom hook to access AuthContext easily
    │   └── useCurricula.js       # Custom hook for Firestore curriculum queries
    ├── utils/
    │   ├── groqApi.js            # Groq API fetch wrapper for curriculum generation
    │   ├── sageApi.js            # Groq API wrapper with Sage system prompt
    │   └── pdfExport.js          # jsPDF logic for multi-page curriculum PDF
    ├── components/
    │   ├── FacultySidebar.jsx    # Left navigation sidebar for faculty role
    │   ├── StudentSidebar.jsx    # Left navigation sidebar for student role
    │   ├── CurriculumCard.jsx    # Card component for curriculum grid display
    │   ├── CurriculumAccordion.jsx # Expandable semester/course display
    │   ├── CommentSection.jsx    # Real-time comments list + post form
    │   ├── RoadmapTimeline.jsx   # Visual timeline for Sage roadmap responses
    │   ├── StatCard.jsx          # Dashboard statistics card component
    │   └── LoadingOverlay.jsx    # Full-screen loading spinner during AI generation
    ├── pages/
    │   ├── Landing.jsx           # Public homepage with hero, features, how it works
    │   ├── Login.jsx             # Email/password login form
    │   ├── Register.jsx          # Registration form with role + college selection
    │   ├── faculty/
    │   │   ├── FacultyLayout.jsx       # Persistent sidebar layout for faculty pages
    │   │   ├── FacultyDashboard.jsx    # Stats overview for faculty
    │   │   ├── GenerateCurriculum.jsx  # AI generation form + results display
    │   │   ├── MyCurricula.jsx         # Table of all faculty curricula
    │   │   ├── GenerationHistory.jsx   # Full generation log with search/filter
    │   │   └── FacultyComments.jsx     # Student feedback viewer
    │   └── student/
    │       ├── StudentLayout.jsx       # Persistent sidebar layout for student pages
    │       ├── StudentDashboard.jsx    # Stats overview for student
    │       ├── BrowseCurricula.jsx     # Grid of published college curricula
    │       ├── CurriculumDetail.jsx    # Full view + download + comments
    │       ├── SageAI.jsx              # Sage chat interface with roadmap generation
    │       ├── SageHistory.jsx         # Past Sage conversations list
    │       ├── MyComments.jsx          # Student's own comments manager
    │       └── ViewHistory.jsx         # Curricula viewing history log
```

---

## 👨‍🏫 How It Works — Faculty Workflow

### Step 1: Register
- Go to `/register`
- Enter: Full Name, Email, Password
- Select Role: Faculty
- Enter College/Organization Name (e.g. "MIT", "VIT Vellore")
- Click Register
- ✅ Firebase creates auth account + Firestore `users/{uid}` document

### Step 2: Login
- Go to `/login`
- Enter email + password
- ✅ Redirected automatically to `/faculty/dashboard`

### Step 3: View Dashboard
- See stats: Total curricula generated, Total published, Total student comments
- College name displayed as badge

### Step 4: Generate a Curriculum
- Click "Generate Curriculum" in sidebar
- Fill the form:
  - Skill: e.g. "Machine Learning"
  - Education Level: Master's / Degree
  - Number of Semesters: 4
  - Weekly Hours: 20-25 (optional)
  - Industry Focus: AI (optional)
- Click "Generate"
- ⏳ Loading overlay appears — "Generating your curriculum..."
- ✅ LLaMA 3.3 70B generates full structured curriculum
- Results display as semester accordion with course cards

### Step 5: Review Results
- Expand each semester to see courses
- Each course shows: name, code, credits, topics (as tags), learning outcomes
- Capstone project shown at bottom

### Step 6: Save or Publish
**Option A — Save as Draft:**
- Click "Save as Draft"
- Saved to Firestore `curricula` collection with `status=draft`
- Only visible to the faculty member
- Saved to `generationHistory` collection

**Option B — Publish to College:**
- Click "Publish to College"
- Saved to Firestore with `status=published`
- ✅ Instantly visible to ALL students registered under same college name
- Saved to `generationHistory` collection

### Step 7: Manage Curricula
- Go to "My Curricula" page
- See all draft and published curricula in a table
- Can: View full curriculum, Publish a draft, Delete any curriculum

### Step 8: View Generation History
- Go to "Generation History" page
- See every generation attempt ever made
- Search by skill name, filter by status, filter by date range
- Click any row to view the full curriculum generated that time

### Step 9: Read Student Feedback
- Go to "Comments" page
- See all comments students have posted on published curricula
- Grouped by curriculum name

---

## 👩‍🎓 How It Works — Student Workflow

### Step 1: Register
- Go to `/register`
- Enter: Full Name, Email, Password
- Select Role: Student
- Enter College Name — must match exactly what faculty used
  ⚠️ **Important:** College name is case-sensitive. "MIT" and "mit" are treated as different colleges.
- Click Register
- ✅ Firebase creates account + Firestore `users/{uid}` document

### Step 2: Login
- Go to `/login`
- Enter email + password
- ✅ Redirected automatically to `/student/dashboard`

### Step 3: View Dashboard
- See stats: Curricula available from college, Sage conversations, Comments made
- College badge confirms which college's data is visible

### Step 4: Browse Curricula
- Click "Browse Curricula" in sidebar
- See grid of all curricula published by faculty from same college
- Filter by: skill name (search), education level, number of semesters
- Click "View Curriculum" on any card

### Step 5: View Curriculum Detail
- Full semester accordion view identical to faculty preview
- See all courses, topics, learning outcomes, capstone project
- ✅ View automatically logged to `viewHistory` collection

### Step 6: Download Curriculum
**Option A — Download PDF:**
- Click "📄 Download PDF"
- Generates multi-page formatted PDF:
  - Page 1: Title page with skill, level, metadata
  - Following pages: Semester tables with course name, code, credits, topics
  - Last page: Capstone project details
- File saved as: `{Skill_Name}_curriculum.pdf`

**Option B — Download JSON:**
- Click `{ } Download JSON`
- Downloads raw structured data
- File saved as: `{Skill_Name}_curriculum.json`
- Useful for developers or LMS integration

### Step 7: Post a Comment
- Scroll below downloads on curriculum detail page
- Read existing comments from other students
- Type in textarea and click "Post Comment"
- ✅ Comment appears in real-time (Firestore `onSnapshot`)
- Faculty can see this in their Comments page

### Step 8: Use Sage AI Study Companion
- Click "Sage AI" in sidebar
- Left panel: select one or more curricula as context
- Type your learning goal: e.g. "I also want to learn Docker and Kubernetes"
- ✅ Sage generates a personalized integrated roadmap:
  - Shows week-by-week plan
  - Highlights where new topics connect to existing courses
  - Suggests resources and tasks
- Chat is multi-turn — ask follow-up questions
- ⚠️ Sage ONLY answers education and curriculum related questions
  - Off-topic questions get: *"I am Sage, your academic study companion..."*

### Step 9: Continue Past Sage Conversations
- Click "Sage History" in sidebar (or transition to History tab)
- See all past conversations with title, date, curricula used
- Click "Continue" to reload full conversation and keep chatting
- Click "Delete" to remove a conversation

### Step 10: Manage Activity
- **My Comments:** view and delete own comments
- **View History:** see all curricula previously viewed with timestamps

---

## 🌿 Sage AI Study Companion

Sage is CurrHub's built-in AI study companion exclusively for students.

### What Sage Does
- Takes the student's existing curriculum as context
- Accepts a new topic the student wants to learn
- Generates an integrated weekly roadmap showing how to learn both simultaneously
- Maintains multi-turn conversation so students can ask follow-up questions

### What Sage Refuses
Sage is fine-tuned to ONLY answer academic and curriculum-related questions. It will refuse and respond with a fixed message for:
- General coding help unrelated to curriculum
- Jokes or casual conversation
- Current events or general knowledge
- Personal advice
- Anything non-educational

### Roadmap Format
Sage returns roadmaps with:
- Weekly breakdown (Week 1, Week 2, etc.)
- Focus area per week
- Tasks and activities
- Integration points with existing semester courses
- Estimated total duration
- Study tips

### Conversation History
Every Sage conversation is saved to Firestore in real-time. Students can return to any past conversation and continue from where they left off.

---

## 🔥 Firebase Structure

CurrHub uses Firestore with 6 collections. All collections are created automatically when first used — no manual setup required.

### Collections Overview

| Collection | Created When | Purpose |
| :--- | :--- | :--- |
| `users` | On register | Stores name, email, role, college |
| `curricula` | Faculty saves/publishes | All curriculum documents |
| `comments` | Student posts comment | Discussion on curricula |
| `generationHistory` | Every AI generation | Full audit log for faculty |
| `sageHistory` | Student uses Sage | Saved AI conversations |
| `viewHistory` | Student views curriculum | Tracking student engagement |

### Document Schemas

#### 1. `users`
```json
{
  "uid": "string (Firebase Auth UID)",
  "name": "string (Full user display name)",
  "email": "string (User email address)",
  "role": "string ('Faculty' | 'Student')",
  "college": "string (Case-sensitive college identifier)",
  "createdAt": "string (ISO 8601 timestamp)"
}
```

#### 2. `curricula`
```json
{
  "skill": "string (Target skill/subject name)",
  "level": "string (Target educational degree level)",
  "semesters": "number (Duration in semester count)",
  "weeklyHours": "number (Committed weekly workload hours)",
  "industryFocus": "string (Target industry focus domain)",
  "generatedData": {
    "skill": "string",
    "level": "string",
    "semesters": "number",
    "weeklyHours": "string",
    "industryFocus": "string",
    "semestersData": [
      {
        "semesterNumber": "number",
        "courses": [
          {
            "courseName": "string",
            "courseCode": "string",
            "credits": "number",
            "weeklyHours": "number",
            "description": "string",
            "topics": ["string"],
            "learningOutcomes": ["string"],
            "learningResources": [
              {
                "title": "string",
                "url": "string",
                "type": "string"
              }
            ]
          }
        ]
      }
    ],
    "capstoneProject": {
      "title": "string",
      "description": "string",
      "deliverables": ["string"]
    }
  },
  "publishedBy": "string (Faculty UID)",
  "publishedByName": "string (Faculty Name)",
  "college": "string (Scope filter college name)",
  "status": "string ('draft' | 'published')",
  "createdAt": "string (ISO 8601 timestamp)",
  "publishedAt": "string | null (ISO 8601 timestamp if status is published)"
}
```

#### 3. `comments`
```json
{
  "curriculumId": "string (Firestore reference ID of curriculum)",
  "curriculumTitle": "string (Skill name of curriculum)",
  "studentUid": "string (Student creator UID)",
  "studentName": "string (Student creator name)",
  "college": "string (Student college filter)",
  "content": "string (Feedback details text)",
  "createdAt": "string (ISO 8601 timestamp)",
  "replies": [
    {
      "facultyName": "string (Faculty replier name)",
      "content": "string (Reply text)",
      "createdAt": "string (ISO 8601 timestamp)"
    }
  ]
}
```

#### 4. `generationHistory`
```json
{
  "facultyUid": "string (Faculty creator UID)",
  "college": "string (Faculty college identifier)",
  "inputs": {
    "skill": "string",
    "level": "string",
    "semesters": "number",
    "weeklyHours": "number | null",
    "industryFocus": "string | null"
  },
  "generatedData": "object (Matches curricula.generatedData schema structure)",
  "status": "string ('generated')",
  "createdAt": "string (ISO 8601 timestamp)"
}
```

#### 5. `sageHistory`
```json
{
  "studentUid": "string (Student creator UID)",
  "college": "string (Student college identifier)",
  "title": "string (Auto-summarized message title)",
  "topic": "string (Goal of roadmap requested)",
  "contextCurriculumIds": ["string (IDs of curricula references used for context)"],
  "messages": [
    {
      "role": "string ('user' | 'assistant')",
      "content": "string (Chat content message)",
      "roadmap": "object | null (Sage formatted learning roadmap nodes)",
      "timestamp": "string (ISO 8601 timestamp)"
    }
  ],
  "createdAt": "string (ISO 8601 timestamp)",
  "updatedAt": "string (ISO 8601 timestamp)"
}
```

#### 6. `viewHistory`
```json
{
  "studentUid": "string (Student UID)",
  "curriculumId": "string (Firestore reference ID of viewed curriculum)",
  "curriculumTitle": "string (Skill name of viewed curriculum)",
  "facultyName": "string (Faculty publisher name)",
  "college": "string (Student college identifier)",
  "viewedAt": "string (ISO 8601 timestamp)"
}
```

---

## 🔐 Environment Variables

Create a `.env` file in the project root. Never commit this file.

| Variable | Where to Get It | What It Does |
| :--- | :--- | :--- |
| `VITE_GROQ_API_KEY` | console.groq.com → API Keys | Authenticates Groq AI calls |
| `VITE_FIREBASE_API_KEY` | Firebase Console → Project Settings | Firebase app identifier |
| `VITE_FIREBASE_AUTH_DOMAIN` | Firebase Console → Project Settings | Firebase auth domain |
| `VITE_FIREBASE_PROJECT_ID` | Firebase Console → Project Settings | Your Firebase project ID |
| `VITE_FIREBASE_STORAGE_BUCKET` | Firebase Console → Project Settings | Firebase storage bucket |
| `VITE_FIREBASE_MESSAGING_SENDER_ID` | Firebase Console → Project Settings | FCM sender ID |
| `VITE_FIREBASE_APP_ID` | Firebase Console → Project Settings | Firebase app ID |

Copy `.env.example` to `.env` and fill in all values before running.

---

## ⚙️ Installation & Setup

### Prerequisites
- Node.js v18 or higher — check with: `node --version`
- npm v9 or higher — check with: `npm --version`
- Git installed
- A Groq account (free at [console.groq.com](https://console.groq.com/))
- A Firebase account (free at [console.firebase.google.com](https://console.firebase.google.com/))

### Step 1: Clone the Repository
```bash
git clone https://github.com/chay2405/curriculumHub-dev.git
cd curriculumHub-dev
```

### Step 2: Install Dependencies
```bash
npm install
```

### Step 3: Setup Environment Variables
```bash
cp .env.example .env
```
*(then fill in all values — see [Environment Variables](#-environment-variables) section)*

---

## 📦 Firebase Setup Guide

1. Go to [console.firebase.google.com](https://console.firebase.google.com/)
2. Create a new project named "currhub"
3. Go to **Authentication** → **Sign-in method** → Enable **Email/Password**
4. Go to **Firestore Database** → **Create database** → Start in test mode
5. Go to **Project Settings** → **Your Apps** → **Add Web App** → Register
6. Copy the config values into your `.env` file

---

## 🔑 Groq API Setup

1. Go to [console.groq.com](https://console.groq.com/)
2. Sign up for free
3. Go to **API Keys** → **Create API Key**
4. Copy the key into `VITE_GROQ_API_KEY` in `.env`

---

## 🚀 Running the Project

1. Run the local development server:
   ```bash
   npm run dev
   ```
   Open [http://localhost:5173](http://localhost:5173) in your browser.

2. Build for production:
   ```bash
   npm run build
   ```

3. Preview production bundle locally:
   ```bash
   npm run preview
   ```

---

## ☁️ Deployment

### Step 1: Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/chay2405/curriculumHub-dev.git
git push -u origin main
```

### Step 2: Deploy on Vercel
1. Go to [vercel.com](https://vercel.com/) and sign in with GitHub
2. Click **"Add New Project"**
3. Import your `currhub` repository
4. Framework Preset: **Vite** (auto-detected)
5. Go to Environment Variables section in Vercel
6. Add ALL 7 variables from your `.env` file one by one
7. Click **Deploy**

### Step 3: Verify Deployment
- Open your Vercel URL
- Register as faculty and student
- Test curriculum generation and Sage AI

⚠️ **Important:** Never add `.env` to git. Always set environment variables directly in Vercel dashboard for production.

---

## ⚠️ Important Notes

1. **College Name Matching**
   Faculty and students MUST register with the exact same college name. "VIT" and "vit" are treated as different colleges. Recommend deciding on a standard format before registering users.

2. **Firestore Test Mode**
   The project uses Firestore in test mode (open read/write). Before going to production, update Firestore security rules to restrict access by authenticated users only.

3. **Groq Free Tier Limits**
   Groq free tier has rate limits. If generation fails, wait 60 seconds and try again. Upgrade to paid tier for production use.

4. **Sage Topic Restriction**
   Sage AI is intentionally restricted to academic topics only. This is enforced via system prompt — it cannot be overridden by users.

5. **PDF Generation**
   PDF is generated entirely client-side using jsPDF. No data is sent to any external service during PDF export.

---
Built with ❤️ using React, Firebase, and Groq AI
