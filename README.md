ZEBE Event Planner 🎉
Live Demo: https://zebe-backend.onrender.com

Overview
ZEBE is a full-stack event planning web app that lets users plan events by selecting venues, catering, and entertainment. It features AI-powered plan generation and an AI chat assistant that recommends real services from the database. Supports Mongolian and English.

Tech Stack
Frontend: React 18, Vite, Tailwind CSS, Axios
Backend: Node.js, Express, MongoDB (Mongoose), JWT + bcryptjs, Anthropic Claude API
DevOps: GitHub Actions, SonarCloud, Docker, Render

CI/CD Pipeline
Every push to main automatically:

Runs SonarCloud code quality analysis
Builds and pushes Docker image to Docker Hub (khosbayera/zebe-webapp)
Triggers Render auto-deploy


Project Structure
ZEBE_eventplanner/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions pipeline
├── Dockerfile                 # Docker build config
├── sonar-project.properties   # SonarCloud config
├── frontend/
│   ├── src/
│   │   ├── components/        # Header, PlannerSection, AIChatSection, etc.
│   │   ├── data/              # mockData.js
│   │   └── App.jsx
│   └── vite.config.js
└── backend/
    ├── controllers/           # authController, eventController
    ├── middleware/            # authMiddleware, errorHandler
    ├── models/                # User, Venue, Catering, Entertainment, SavedPlan
    ├── routes/                # auth, event, plan, chat
    ├── public/                # Built frontend (auto-generated)
    ├── seed.js
    └── server.js

API Endpoints
MethodEndpointDescriptionAuthPOST/api/auth/registerRegister userNoPOST/api/auth/loginLogin, returns JWTNoPOST/api/plan-eventGenerate 3 event plansYesGET/api/venuesList venuesNoGET/api/cateringList catering optionsNoGET/api/entertainmentList entertainmentNoGET/api/plansGet saved plansYesPOST/api/plansSave a planYesDELETE/api/plans/:idDelete a planYesPOST/api/chatAI chat assistantYesGET/api/healthHealth checkNo

Environment Variables
Create a .env in backend/:
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d
ANTHROPIC_API_KEY=your_anthropic_api_key
PORT=5001

Local Development
bash# Install
cd backend && npm install
cd ../frontend && npm install

# Seed database
cd backend && node seed.js

# Run backend (port 5001)
cd backend && npm run dev

# Run frontend (port 3000)
cd frontend && npm run dev

Deploying to Render
Root Directory: (blank)
Build Command:
bashcd frontend && npm install && npm run build && cd ../backend && npm install
Start Command:
bashnode backend/server.js
Add all .env variables in Render's Environment settings.

Features

JWT-based auth (register/login)
AI plan generator — 3 budget-tiered event plans
Service explorer — browse venues, catering, entertainment
AI chat assistant powered by Claude (recommends real DB services)
Save, view, and delete event plans
Bilingual UI (Mongolian + English) with Mongolian ornament design
Full CI/CD pipeline with SonarCloud + Docker + Render


Common Issues
Frontend changes not showing on Render:
bashcd frontend && npm run build
git add . && git commit -m "rebuild" && git push
MongoDB not connecting — check MONGO_URI in Render env vars and allow all IPs (0.0.0.0/0) in Atlas.
AI chat not working — check ANTHROPIC_API_KEY is set in Render env vars.
