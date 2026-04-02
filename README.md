# Whop

![Project: Whop](https://img.shields.io/badge/Whop-ready-blue)
![Status](https://img.shields.io/badge/status-beta-yellow)
![License](https://img.shields.io/badge/license-ISC-lightgrey)

## Table of Contents

- [What the project does](#what-the-project-does)
- [Why the project is useful](#why-the-project-is-useful)
- [Architecture](#architecture)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Backend setup](#backend-setup)
  - [Frontend setup](#frontend-setup)
  - [Run the full stack](#run-the-full-stack)
- [API endpoints (summary)](#api-endpoints-summary)
- [Usage examples](#usage-examples)
- [Environment variables](#environment-variables)
- [Screenshots](#screenshots)
- [Deployment links](#deployment-links)
- [Where users can get help](#where-users-can-get-help)
- [Who maintains this project](#who-maintains-this-project)

## What the project does

**Whop** is a full-stack real-time chat application (Node.js/Express + React/Vite with TypeScript) that enables users to communicate instantly with message history, user profiles, and real-time notifications.

It supports user authentication (Passport JWT), creation of chat rooms/conversations, message persistence, image uploads to Cloudinary, and live messaging via Socket.io. All messages and user data are stored in MongoDB for reliable access.

## Why the project is useful

- Real-time messaging with instant delivery via Socket.io
- Persistent chat history stored in MongoDB
- User authentication and authorization with JWT
- Image upload support via Cloudinary for rich media sharing
- TypeScript for type safety across the stack
- Modern UI with Tailwind CSS and Radix UI components
- Responsive design that works on desktop and mobile
- Dark/Light theme support

## Architecture

- Backend: `backend/`
  - Express server (TypeScript) in `src/index.ts`
  - Auth routes: `src/routes/` with Passport JWT strategy
  - Socket.io integration in `src/lib/socket.ts` for real-time messaging
  - Controllers: `src/controllers/` for auth, chat, message, user logic
  - Models: `src/models/` with Mongoose schemas
  - Middleware for error handling, async handlers, and authentication
  - Database config in `src/config/database.config.ts`
- Frontend: `client/`
  - React app with Vite + TypeScript
  - Routing via React Router
  - State management with Zustand
  - Real-time socket client in `src/` components
  - Tailwind CSS + Radix UI for styling
  - Form validation with React Hook Form + Zod

## Getting started

### Prerequisites

- Node.js 18+ (or latest LTS)
- npm 10+ (or yarn)
- MongoDB instance (Atlas or local)
- Cloudinary account (for image uploads)
- For dev, use two shells (backend and frontend)

### Backend setup

```bash
cd D:\Whop\backend
npm install
```

Create `.env` in `backend/` with:

```env
PORT=5000
MONGODB_URI="<your-mongodb-connection-string>"
JWT_SECRET="<strong-jwt-secret>"
NODE_ENV=development
FRONTEND_ORIGIN="http://localhost:5173"
CLOUDINARY_CLOUD_NAME="<your-cloudinary-name>"
CLOUDINARY_API_KEY="<your-cloudinary-api-key>"
CLOUDINARY_API_SECRET="<your-cloudinary-api-secret>"
```

Start the backend:

```bash
npm run dev
```

### Frontend setup

```bash
cd D:\Whop\client
npm install
```

Create `.env.local` in `client/` with:

```env
VITE_API_BASE_URL=http://localhost:5000
```

Start frontend:

```bash
npm run dev
```

### Run the full stack

1. Start backend (`npm run dev` in `backend/`).
2. Start frontend (`npm run dev` in `client/`).
3. Open the app at `http://localhost:5173`.

## API endpoints (summary)

### Auth

- `POST /api/auth/register` - Register new user (username, email, password).
- `POST /api/auth/login` - Login user (email, password). Returns JWT in cookie.
- `POST /api/auth/logout` - Logout and clear session.
- `GET /api/auth/me` - Get current authenticated user details (protected).

### Users

- `GET /api/users` - Get list of all users (protected).
- `GET /api/users/:userId` - Get user details by ID (protected).
- `PUT /api/users/:userId` - Update user profile (protected).

### Chat

- `POST /api/chat` - Create new chat/conversation (protected).
- `GET /api/chat` - Get all chats for authenticated user (protected).
- `GET /api/chat/:chatId` - Get chat details by ID (protected).

### Messages

- `POST /api/messages` - Send message to chat (protected, can include images).
- `GET /api/messages/:chatId` - Get messages in a chat (protected).
- `DELETE /api/messages/:messageId` - Delete message (protected).

## Usage examples

### Register

```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"alice","email":"alice@example.com","password":"Secret123"}'
```

### Login

```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"alice@example.com","password":"Secret123"}' \
  -c cookies.txt
```

### Create chat

```bash
curl -X POST http://localhost:5000/api/chat \
  -H "Content-Type: application/json" \
  -b cookies.txt \
  -d '{"participantIds":["userId1","userId2"]}'
```

### Send message

```bash
curl -X POST http://localhost:5000/api/messages \
  -H "Content-Type: application/json" \
  -b cookies.txt \
  -d '{"chatId":"<chatId>","content":"Hello!","type":"text"}'
```

### Fetch messages

```bash
curl -X GET http://localhost:5000/api/messages/<chatId> -b cookies.txt
```

## Environment variables

- Backend (`backend/.env`)
  - `PORT` (default `5000`)
  - `MONGODB_URI`
  - `JWT_SECRET`
  - `NODE_ENV` (development/production)
  - `FRONTEND_ORIGIN`
  - `CLOUDINARY_CLOUD_NAME`
  - `CLOUDINARY_API_KEY`
  - `CLOUDINARY_API_SECRET`

- Frontend (`client/.env.local`)
  - `VITE_API_BASE_URL` (e.g., `http://localhost:5000`)

## Screenshots

- ![Login screen](docs/screenshots/login.png)
- ![Chat dashboard](docs/screenshots/chat-dashboard.png)
- ![Chat conversation](docs/screenshots/chat-conversation.png)
- ![User profile](docs/screenshots/user-profile.png)

## Deployment links

- Frontend: [https://whop-frontend.onrender.com]
- Backend: [https://whop-backend-nutz.onrender.com]

> Note: Deployment may be on a sleep/idle plan. The first request can take ~60 seconds while the service wakes up.

## Where users can get help

- Project issues: open an issue in the repository.
- Check source code in `backend/src/` and `client/src/`.
- Collect debug info: backend server logs, browser dev tools, network tab, Socket.io events.
- For library docs:
  - Express: https://expressjs.com/
  - Socket.io: https://socket.io/docs/
  - React (Vite): https://vitejs.dev/guide/
  - Mongoose: https://mongoosejs.com/
  - TypeScript: https://www.typescriptlang.org/docs/

## Who maintains this project

Maintainer: [Pranjal Verma].

> Personal project for resume/portfolio purposes. Keep deployment concise and this README focused on onboarding/app demonstration.

---

> Note: This README intentionally focuses on quick developer onboarding. Detailed API docs and troubleshooting should live in separate docs/Wiki pages to keep the core README compact.
