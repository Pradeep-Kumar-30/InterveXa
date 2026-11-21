# FresherAI Frontend

This directory contains the React and Vite frontend for FresherAI.

## Development

Install dependencies and start the Vite development server:

```powershell
npm install
npm run dev
```

The frontend expects `frontend/.env` to contain:

```env
VITE_FIREBASE_APIKEY=your_firebase_web_api_key
VITE_RAZORPAY_KEY_ID=your_razorpay_public_key
VITE_BACKEND_URL=http://localhost:8000
```

## Available Scripts

| Command | Purpose |
|---|---|
| `npm run dev` | Start the development server |
| `npm run build` | Create the production build |
| `npm run lint` | Run ESLint |
| `npm run preview` | Preview the production build locally |

## Main Areas

- Authentication and landing experience
- Candidate dashboard and performance charts
- Resume analysis and resume builder
- Interview setup, live interview flow, and reports
- Personalized roadmap viewer
- Razorpay billing integration

See the [project README](../README.md) for the complete architecture, environment setup, backend services, API routes, and deployment guidance.
