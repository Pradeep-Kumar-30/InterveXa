<!-- by pradeep -->
# InterveXa

<p align="center">
  <img src="frontend/public/logo.png" alt="InterveXa logo" width="120">
</p>

<p align="center">
  <strong>An AI-powered interview preparation platform for building resumes, practicing interviews, receiving feedback, and following personalized learning roadmaps.</strong>
</p>

## Overview

InterveXa is a full-stack career preparation platform built around specialized AI agents. It combines Firebase authentication, MongoDB data storage, Redis caching, Groq-powered language models, YouTube resources, and Razorpay payments in a microservices architecture.

Users can:

- Sign in securely with Google
- Upload a resume and receive ATS-style analysis and improvement feedback
- Build a polished resume using guided forms and a printable preview
- Practice HR, technical, and coding interviews
- Receive interview reports and performance scores
- Track interview history and average performance
- Generate goal-based learning roadmaps
- Purchase interview credits through Razorpay

## Features

### Resume Intelligence

- PDF resume upload and parsing
- AI-generated strengths, weaknesses, and improvement suggestions
- Guided resume builder with personal, education, experience, project, and skills sections
- Printable resume preview
- ATS-focused resume scoring

### AI Interview Agent

- Step-by-step interview setup
- HR, technical, and coding interview modes
- AI-generated questions and contextual follow-ups
- Answer submission and interview progress tracking
- Final performance report with detailed scores

### Learning Roadmap Agent

- Personalized roadmap generation
- Skill and goal-based learning modules
- Curated YouTube resources
- Saved roadmap history

### Performance Dashboard

- Total interview, question, and completion metrics
- Technical and HR performance history
- Average interview score
- Visualized progress charts

### Authentication and Billing

- Firebase Google authentication
- Protected API routes
- User interview credits
- Razorpay order creation and payment verification

## Architecture

```text
Frontend (React + Vite)
        |
        v
API Gateway (Express)
        |
        +--> Auth Service
        +--> Resume Service
        +--> Interview Service
        +--> Roadmap Service
        +--> Billing Service

Shared infrastructure:
Redis | MongoDB | Firebase Admin | Groq | YouTube API | Razorpay
```

| Component | Technology | Default Port |
|---|---|---:|
| Frontend | React, Vite, Tailwind CSS, Redux | `5173` |
| API Gateway | Express | `8000` |
| Auth Service | Express, Firebase Admin, MongoDB | `8001` |
| Resume Service | Express, Groq, PDF parsing | `8002` |
| Interview Service | Express, Groq, LangGraph | `8003` |
| Roadmap Service | Express, Groq, YouTube API | `8004` |
| Billing Service | Express, Razorpay | `8005` |
| Redis | Docker Redis | `6379` |

## Tech Stack

### Frontend

- React 19
- Vite
- React Router
- Redux Toolkit
- Tailwind CSS
- Firebase Authentication
- Axios
- Monaco Editor
- Recharts
- Motion

### Backend

- Node.js and ES modules
- Express 5
- MongoDB and Mongoose
- Redis and ioredis
- Firebase Admin
- LangChain and Groq
- LangGraph
- Razorpay
- Multer and PDF parsing

## Project Structure

```text
InterveXa/
├── frontend/
│   ├── public/
│   └── src/
│       ├── apis/
│       ├── components/
│       ├── pages/
│       ├── redux/
│       └── utils/
└── backend/
    ├── gateway/
    ├── services/
    │   ├── auth/
    │   ├── billing/
    │   ├── interview/
    │   ├── resume/
    │   └── roadmap/
    ├── shared/
    └── docker-compose.yml
```

## Prerequisites

Install the following before running the project:

- Node.js 20 or newer
- npm
- MongoDB, local or MongoDB Atlas
- Docker Desktop, for Redis
- A Firebase project
- A Groq API key
- A YouTube Data API key
- A Razorpay account

## Environment Configuration

Do not commit real credentials or service-account files. The repository ignores `.env`, `.env.*`, and `**/serviceAccountKey.json`.

### Frontend: `frontend/.env`

```env
VITE_FIREBASE_APIKEY=your_firebase_web_api_key
VITE_RAZORPAY_KEY_ID=your_razorpay_public_key
VITE_BACKEND_URL=http://localhost:8000
```

### API Gateway: `backend/gateway/.env`

```env
PORT=8000
REDIS_URL=redis://localhost:6379
AUTH_SERVICE_URL=http://localhost:8001
RESUME_SERVICE_URL=http://localhost:8002
INTERVIEW_SERVICE_URL=http://localhost:8003
ROADMAP_SERVICE_URL=http://localhost:8004
BILLING_SERVICE_URL=http://localhost:8005
FRONTEND_URL=http://localhost:5173
```

### Auth Service: `backend/services/auth/.env`

```env
PORT=8001
MONGODB_URL=your_mongodb_connection_string/user
REDIS_URL=redis://localhost:6379
```

Place the Firebase Admin service-account JSON at:

```text
backend/services/auth/serviceAccountKey.json
```

Enable Google sign-in in Firebase Authentication and add `localhost` to the authorized domains.

### Resume Service: `backend/services/resume/.env`

```env
PORT=8002
MONGODB_URL=your_mongodb_connection_string/resume
REDIS_URL=redis://localhost:6379
GROQ_API_KEY=your_groq_api_key
```

### Interview Service: `backend/services/interview/.env`

```env
PORT=8003
MONGODB_URL=your_mongodb_connection_string/interview
REDIS_URL=redis://localhost:6379
GROQ_API_KEY=your_groq_api_key
```

### Roadmap Service: `backend/services/roadmap/.env`

```env
PORT=8004
MONGODB_URL=your_mongodb_connection_string/roadmap
REDIS_URL=redis://localhost:6379
GROQ_API_KEY=your_groq_api_key
YOUTUBE_API_KEY=your_youtube_data_api_key
```

### Billing Service: `backend/services/billing/.env`

```env
PORT=8005
MONGODB_URL=your_mongodb_connection_string/billing
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
```

## Local Installation

Clone the repository and install dependencies in each package:

```powershell
git clone <repository-url>
cd InterveXa

npm install --prefix frontend
npm install --prefix backend/gateway
npm install --prefix backend/services/auth
npm install --prefix backend/services/resume
npm install --prefix backend/services/interview
npm install --prefix backend/services/roadmap
npm install --prefix backend/services/billing
```

Start Redis:

```powershell
cd backend
docker compose up -d redis
```

Create the environment files described above, then start each process in a separate terminal.

```powershell
# Terminal 1 - API gateway
cd backend/gateway
npm run dev
```

```powershell
# Terminal 2 - Auth
cd backend/services/auth
npm run dev
```

```powershell
# Terminal 3 - Resume
cd backend/services/resume
npm run dev
```

```powershell
# Terminal 4 - Interview
cd backend/services/interview
npm run dev
```

```powershell
# Terminal 5 - Roadmap
cd backend/services/roadmap
npm run dev
```

```powershell
# Terminal 6 - Billing
cd backend/services/billing
npm run dev
```

```powershell
# Terminal 7 - Frontend
cd frontend
npm run dev
```

Open `http://localhost:5173`.

## API Routes

The frontend communicates with the platform through `http://localhost:8000`.

| Feature | Route | Method |
|---|---|---|
| Google login | `/api/auth/login` | `POST` |
| Logout | `/api/auth/logout` | `GET` |
| Current user | `/api/me` | `GET` |
| Resume upload and analysis | `/api/resume/upload` | `POST` |
| Get saved resume | `/api/resume/get-resume` | `GET` |
| Start interview | `/api/interview/start` | `POST` |
| Submit answer | `/api/interview/answer` | `POST` |
| Interview history | `/api/interview/all` | `GET` |
| Interview details | `/api/interview/:id` | `GET` |
| Generate roadmap | `/api/roadmap/generate` | `POST` |
| Roadmap history | `/api/roadmap/all` | `GET` |
| Roadmap details | `/api/roadmap/:id` | `GET` |
| Create payment order | `/api/billing/create` | `POST` |
| Verify payment | `/api/billing/verify` | `POST` |

Resume, interview, roadmap, billing, and current-user routes require authentication middleware.

## Production Build

Build the frontend:

```powershell
cd frontend
npm run build
```

The optimized static build is written to `frontend/dist`.

For production deployment:

1. Build and serve the frontend through a static host or reverse proxy.
2. Deploy Redis as a managed or containerized service.
3. Replace local MongoDB URLs with secure Atlas or managed database URLs.
4. Deploy each Express service with its environment variables.
5. Point `VITE_BACKEND_URL` and `FRONTEND_URL` to production domains.
6. Enable the relevant Firebase and Razorpay origins/domains.
7. Restrict CORS, secrets, database access, and API keys to the intended environment.

## Validation

Run the frontend lint and production build checks:

```powershell
cd frontend
npm run lint
npm run build
```

There is no automated test suite configured in the backend package manifests.

## Security Notes

- Never commit Firebase credentials, Razorpay secrets, Groq keys, MongoDB URLs, or service-account JSON.
- Keep Firebase and Razorpay credentials in environment-specific configuration.
- Use HTTPS and secure cookies in production.
- Rotate any credential that has been exposed in a shared environment.
- Configure MongoDB network access and database users with the least required privileges.

## Troubleshooting

### Redis connection fails

Confirm Docker Desktop is running and Redis is available:

```powershell
cd backend
docker compose up -d redis
docker compose ps
```

### MongoDB connection fails

Verify `MONGODB_URL`, database user credentials, network allow-list settings, and that the database name in the connection string matches the service.

### Firebase authentication fails

Verify `VITE_FIREBASE_APIKEY`, Google sign-in configuration, localhost authorization, and the Firebase Admin `serviceAccountKey.json` file.

### Groq or YouTube features fail

Confirm the relevant API keys and account quotas. Check the specific service terminal for provider errors.

### Razorpay verification fails

Ensure the same Razorpay key pair is configured in `frontend/.env` and `backend/services/billing/.env`, and use the matching mode for development or production.
