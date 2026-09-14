# Sports Tournament Management System

A full-stack platform for organizing, managing, and publicly tracking sports tournaments. The project includes an admin panel, an organizer panel, a referee panel, and public-facing pages for viewers.

## Live Demo

🔗 https://sistem-per-menaxhimin-e-turneut-sportiv-3gei-g8zrsjj9x.vercel.app

## Overview

The application helps manage the main lifecycle of a sports tournament:

- creating sports, teams, players, venues, and tournaments
- registering teams into tournaments
- scheduling matches and assigning referees
- recording results and live match events
- public tournament standings
- generating and publicly displaying knockout brackets
- role-based authentication for admin, organizer, and referee

## Key Features

- **Authentication and sessions**: login/register with a token cookie for short-lived JWTs and a sessionId cookie for persistent sessions.
- **Roles and access**: admin, organizer, referee, and public user.
- **Tournament management**: creating tournaments, linked to sport, venue, dates, and organizer.
- **Team and player management**: team registration, player profiles, linked to the relevant sport.
- **Live matches**: real-time updates via Socket.IO and a cron job for match status updates.
- **Results and standings**: storing results, winners, MVPs, and standings tables.
- **Knockout brackets**: generation, seeding, match scheduling, and winner advancement.
- **Public pages**: live matches, standings, brackets, and players — no login required.
- **Contact and password reset**: contact form and email-based password recovery.

## Tech Stack

**Frontend**
- React
- Vite
- React Router
- Tailwind CSS
- Axios
- Socket.IO Client
- Framer Motion
- Lucide React / React Icons

**Backend**
- Node.js
- Express
- PostgreSQL
- Prisma
- Socket.IO
- JWT
- Cookie Parser
- Joi
- Nodemailer
- Node Cron

## Project Structure

```
.
├── backend/
│   ├── prisma/
│   │   └── schema.prisma
│   ├── src/
│   │   ├── config/
│   │   ├── lib/
│   │   ├── middleware/
│   │   ├── routes/
│   │   ├── services/
│   │   └── server.js
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── config/
│   │   ├── context/
│   │   ├── pages/
│   │   ├── socket.js
│   │   └── App.jsx
│   └── package.json
└── README.md
```

## Requirements

Before running the project, make sure you have:

- Node.js installed
- PostgreSQL installed with a database created
- npm
- database credentials
- optionally, a Gmail app password for sending password-reset emails

## Local Setup

### 1. Clone the project

```
git clone <repo-url>
cd Sistem-per-Menaxhimin-e-Turneut-Sportiv
```

### 2. Install dependencies

Backend:

```
cd backend
npm install
```

Frontend:

```
cd ../frontend
npm install
```

### 3. Configure the backend

Create a `.env` file inside `backend/`:

```
PORT=3005
CLIENT_URL=http://localhost:5173

DATABASE_URL="postgresql://postgres:password@localhost:5432/tournament_db?schema=public"

DB_HOST=localhost
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=tournament_db
DB_PORT=5432

JWT_SECRET=change_this_secret

EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_gmail_app_password
NODE_ENV=development
```

`DATABASE_URL` is used by Prisma. The `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, and `DB_PORT` variables are used by the existing `pg` connection in the backend.

### 4. Configure the frontend

Create a `.env` file inside `frontend/`:

```
VITE_API_URL=http://localhost:3005
```

Note: the frontend defaults to `http://localhost:5000`, while the backend defaults to `3005`. Because of this, set `VITE_API_URL=http://localhost:3005`, or change `PORT` in the backend as needed.

### 5. Generate the Prisma client

From the `backend/` folder:

```
npx prisma generate
```

If you're creating the database from scratch, use whichever approach fits your setup:

```
npx prisma migrate dev
```

or:

```
npx prisma db push
```

## Running the Project

Open two terminals.

**Terminal 1 — backend:**

```
cd backend
npm run dev
```

The backend usually starts at:

```
http://localhost:3005
```

**Terminal 2 — frontend:**

```
cd frontend
npm run dev
```

The frontend usually starts at:

```
http://localhost:5173
```

## Useful Commands

**Frontend:**

```
npm run dev
npm run build
npm run lint
npm run preview
```

**Backend:**

```
npm run dev
npx prisma generate
npx prisma studio
```

Currently the `npm test` script in the backend is a placeholder, and there is no test suite configured.

## Main Routes

**Public pages**
- `/` - homepage
- `/live-matches` - live matches
- `/public/standings` - public standings
- `/brackets` or `/public/brackets` - public brackets
- `/public/players` - public players
- `/contact-us` - contact

**Admin**
- `/dashboard`
- `/sports`
- `/teams`
- `/players`
- `/venues`
- `/matches`
- `/match-results`
- `/match-referees`
- `/tournaments`
- `/referees`
- `/standings`
- `/admin/brackets`
- `/admin/live-matches`
- `/users`
- `/sessions`

**Organizer**
- `/organizer/dashboard`
- `/organizer/tournaments`
- `/organizer/matches`
- `/organizer/live-matches`
- `/organizer/teams`
- `/organizer/standings`
- `/organizer/brackets`

**Referee**
- `/referee/dashboard`
- `/referee/matches`
- `/referee/live-matches`
- `/referee/match-results`

## Main API

The backend mounts several main routers:

- `/api/auth` - login, register, refresh, logout, reset password
- `/sports`
- `/players`
- `/users`
- `/venues`
- `/teams`
- `/matches`
- `/match-events`
- `/tournaments`
- `/match-results`
- `/match-referees`
- `/tournament-registrations`
- `/referees`
- `/standings`
- `/brackets`
- `/contactUs`
- `/sessions`
- `/profile`
- `/dashboard`

## Authentication

After login/register, the backend sets two cookies:

- **token**: a short-lived JWT used for protected requests.
- **sessionId**: the session ID stored in the database, used to refresh the token.

The `/api/auth/refresh` endpoint verifies the `sessionId` and issues a new token if the session is still valid.

## Development Notes

- Make sure PostgreSQL is running before starting the backend.
- Make sure `CLIENT_URL` in the backend matches the frontend's URL.
- Make sure `VITE_API_URL` in the frontend matches the backend's URL.
- For cookie-based auth, frontend requests must include credentials/cookies.
- Socket.IO uses the same `VITE_API_URL` as the API.
- For password reset via Gmail, use an app password, not your regular email password.

## License

This project was created for academic and development purposes.