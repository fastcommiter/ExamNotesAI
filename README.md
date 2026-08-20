# 📚 ExamNotesAI

**ExamNotesAI** is an AI-powered study assistant built using the **MERN stack** that helps students generate exam-focused notes and answers from a given topic.

The application uses **Generative AI** to create structured study material based on the student's topic, class level, and exam type. It also includes authentication, credit-based usage, and a payment-ready system.

---

## 🚀 Features

* 🤖 **AI-Powered Note Generation**

  * Generate structured notes using Generative AI.
  * Create exam-focused answers from a topic.
  * Supports different class levels and exam types.

* 🔐 **Authentication & Authorization**

  * User registration and login.
  * JWT-based authentication.
  * Authentication handled using secure **HTTP-only cookies**.
  * Protected routes using authentication middleware.

* 💳 **Credit-Based System**

  * Users receive credits for generating AI content.
  * Different credit packages are available.
  * Credit balance can be managed based on usage.

* 💰 **Payment System**

  * Pricing page with multiple credit plans.
  * Selected plan tracking.
  * Payment processing flow integrated into the application.

* 📊 **User Dashboard**

  * Displays user-related information.
  * Shows available credits.
  * Provides access to generated study material.

* ⚡ **Loading & Progress UI**

  * Dynamic progress indicator while AI notes are being generated.
  * Different progress messages such as:

    * Generating notes...
    * Processing contents...
    * Finalizing notes...
    * Almost Done...

* 📱 **Responsive UI**

  * Responsive design using Tailwind CSS.
  * Works across desktop and mobile screen sizes.

---

## 🛠️ Tech Stack

### Frontend

* React.js
* React Router
* Tailwind CSS
* Framer Motion / Motion
* Axios

### Backend

* Node.js
* Express.js
* JWT
* Cookie-based Authentication
* REST APIs

### Database

* MongoDB
* MongoDB Atlas
* Mongoose

### AI

* Generative AI / Gemini API
* Prompt-based content generation

### Other

* Git & GitHub
* Vercel / Render for deployment

---

## 🏗️ Project Architecture

```text
                    ┌─────────────────────┐
                    │       User          │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   React Frontend    │
                    │                     │
                    │  • Dashboard        │
                    │  • Notes Generator  │
                    │  • Pricing          │
                    │  • Authentication   │
                    └──────────┬──────────┘
                               │
                         REST API / Axios
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Express Backend   │
                    │                     │
                    │  • Auth Middleware  │
                    │  • Controllers      │
                    │  • Routes            │
                    │  • AI Integration   │
                    └───────┬─────┬───────┘
                            │     │
                  ┌─────────┘     └─────────┐
                  ▼                         ▼
        ┌──────────────────┐       ┌──────────────────┐
        │ MongoDB Atlas    │       │  Gemini API      │
        │                  │       │                  │
        │ Users            │       │ AI Notes         │
        │ Credits          │       │ AI Answers       │
        │ Data             │       │ Generation       │
        └──────────────────┘       └──────────────────┘
```

---

## 🔐 Authentication Flow

ExamNotesAI uses JWT-based authentication with HTTP-only cookies.

```text
User Login
    ↓
Backend validates credentials
    ↓
JWT Token generated
    ↓
Token stored in HTTP-only Cookie
    ↓
Browser automatically sends Cookie
    ↓
isAuth Middleware
    ↓
Token Verification
    ↓
Protected Route Access
```

### Cookie Configuration

In production, secure cookie settings are used:

```javascript
res.cookie("token", token, {
    httpOnly: true,
    secure: true,
    sameSite: "none",
    maxAge: 7 * 24 * 60 * 60 * 1000
});
```

`httpOnly` prevents client-side JavaScript from directly accessing the authentication cookie.

`secure: true` ensures the cookie is transmitted only over HTTPS.

`sameSite: "none"` allows the cookie to be sent in cross-site requests when the frontend and backend are deployed on different origins.

---

## 🤖 AI Note Generation Flow

```text
User enters:
    ↓
Topic
Class Level
Exam Type
    ↓
Frontend sends API request
    ↓
Express Backend
    ↓
Validate User
    ↓
Check Credits
    ↓
Generate Prompt
    ↓
Gemini API
    ↓
AI Generated Content
    ↓
Backend Response
    ↓
Frontend
    ↓
Display Notes
```

---

## 💳 Credit System

The application follows a credit-based model.

Users can purchase different credit packages:

| Plan        | Credits     |
| ----------- | ----------- |
| Starter     | 50 Credits  |
| Popular     | 320 Credits |
| Pro Learner | 650 Credits |

When a user generates AI content, the required credits can be deducted from their account.

This approach helps control AI API usage and provides a foundation for monetization.

---

## 📁 Project Structure

```text
ExamNotesAI/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── context/
│   │   └── App.jsx
│   │
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── config/
│   ├── server.js
│   └── package.json
│
└── README.md
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/ExamNotesAI.git

cd ExamNotesAI
```

### 2. Install Frontend Dependencies

```bash
cd frontend
npm install
```

### 3. Install Backend Dependencies

```bash
cd ../backend
npm install
```

---

## 🔑 Environment Variables

Create a `.env` file inside the backend directory.

```env
PORT=5000

MONGO_URI=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

GEMINI_API_KEY=your_gemini_api_key

FRONTEND_URL=http://localhost:5173
```

Never commit your `.env` file to GitHub.

Add it to `.gitignore`:

```text
.env
node_modules
```

---

## ▶️ Running the Project

### Start Backend

```bash
cd backend
npm run dev
```

### Start Frontend

Open another terminal:

```bash
cd frontend
npm run dev
```

The application will then be available through the Vite development server.

---

## 🌐 Deployment

The frontend and backend can be deployed separately.

Example architecture:

```text
React Frontend
      │
      │ HTTPS
      ▼
Vercel
      │
      │ API Requests
      ▼
Express Backend
      │
      ├── MongoDB Atlas
      │
      └── Gemini API
```

For production authentication, secure cookies and CORS configuration are used.

---

## 🔒 Security

The project implements several security practices:

* JWT authentication
* HTTP-only cookies
* Secure cookies in production
* Protected backend routes
* Environment variables for API keys
* CORS configuration
* Authentication middleware
* Server-side validation

---

## 🎯 Future Improvements

* 📄 PDF export for generated notes
* 📝 AI-generated quizzes
* 🎯 Personalized study plans
* 📈 Learning progress tracking
* 🧠 Adaptive question generation
* 💳 Complete payment gateway integration
* ☁️ Cloud-based file storage
* 📊 Advanced analytics dashboard

---

## 👨‍💻 Author

**Kunal Latwal**

MCA (AI & Data Science)
Full-Stack Developer | AI/ML Enthusiast

---

## ⭐ Project Highlights

**ExamNotesAI demonstrates practical implementation of:**

* MERN Stack Development
* REST API Design
* JWT Authentication
* HTTP-only Cookie Authentication
* MongoDB Atlas
* Generative AI Integration
* Credit-Based Architecture
* Payment System Design
* Protected Routes
* Responsive UI
* Production Deployment
