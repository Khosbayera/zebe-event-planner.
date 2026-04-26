# ZEBE Event Planner

Live Demo: https://zebe-backend.onrender.com

---

## Overview

ZEBE is a full-stack event planning web app that lets users plan events by selecting venues, catering, and entertainment. It includes AI-powered plan generation and an AI chat assistant that recommends real services from the database. The app supports both Mongolian and English.

---

## Tech Stack

Frontend:

* React 18
* Vite
* Tailwind CSS
* Axios

Backend:

* Node.js
* Express
* MongoDB (Mongoose)
* JWT authentication
* bcryptjs
* Anthropic Claude API

Deployment:

* Render (monorepo setup, frontend served from backend)

---

## Project Structure

ZEBE_eventplanner/

frontend/

* src/

  * components/ (Header, PlannerSection, AIChatSection, etc.)
  * data/ (mockData.js)
  * App.jsx
* vite.config.js

backend/

* controllers/ (authController, eventController)
* middleware/ (authMiddleware, errorHandler)
* models/ (User, Venue, Catering, Entertainment, SavedPlan)
* routes/ (auth, event, plan, chat)
* public/ (built frontend files)
* seed.js
* server.js

---

## API Endpoints

POST /api/auth/register → Register user
POST /api/auth/login → Login and get JWT
POST /api/plan-event → Generate event plans (auth required)

GET /api/venues → Get venues
GET /api/catering → Get catering options
GET /api/entertainment → Get entertainment

GET /api/plans → Get saved plans (auth required)
POST /api/plans → Save a plan (auth required)
DELETE /api/plans/:id → Delete a plan (auth required)

POST /api/chat → AI chat assistant (auth required)
GET /api/health → Health check

---

## Environment Variables

Create a .env file inside backend folder:

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d
ANTHROPIC_API_KEY=your_anthropic_api_key
PORT=5001

---

## Local Development

Install dependencies:

cd backend
npm install

cd ../frontend
npm install

Seed database:

cd backend
node seed.js

Run backend:

cd backend
npm run dev

Run frontend:

cd frontend
npm run dev

---

## Deploying to Render

Build Command:

cd frontend && npm install && npm run build && cd ../backend && npm install

Start Command:

node backend/server.js

vite.config.js update:

build:
outDir: '../backend/public'
emptyOutDir: true

Add environment variables in Render dashboard.

---

## Features

* User authentication (JWT)
* AI-powered event plan generation
* Service explorer (venues, catering, entertainment)
* AI chat assistant (Claude API)
* Save and manage event plans
* Bilingual interface (Mongolian and English)

---

## Common Issues

Frontend not updating:
cd frontend && npm run build
git add .
git commit -m "rebuild"
git push

MongoDB not connecting:
Check MONGO_URI and allow IP 0.0.0.0/0 in MongoDB Atlas

AI chat not working:
Check ANTHROPIC_API_KEY in environment variables
