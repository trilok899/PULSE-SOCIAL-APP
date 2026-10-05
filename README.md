# Pulse – Modern Social Network

Pulse is a full-stack social media application where users can create posts, like, comment, follow others, and explore content.

## Features

- **Authentication**: Register, Login, JWT-based protected routes
- **Feed**: Chronological home feed with posts from followed users + own posts
- **Posts**: Create text posts (image URL support), edit, delete
- **Engagement**: Like / Unlike posts, add comments
- **Social Graph**: Follow / Unfollow users
- **Profiles**: Public profiles with posts, follower/following counts
- **Search**: Search users by name or username
- **Notifications**: Basic like & follow notifications
- **Responsive UI**: Fully responsive (desktop, tablet, mobile)
- **Modern Design**: Clean indigo-accented interface with Tailwind CSS

## Technology Stack

### Frontend
- React 18 + Vite
- React Router v6
- Tailwind CSS
- Axios
- Lucide React (icons)
- React Hot Toast (notifications)

### Backend
- Node.js + Express.js
- MySQL (mysql2)
- JWT + bcryptjs
- express-validator
- cors, helmet, morgan
- dotenv

### Database
- MySQL 8

### Automation
Separated worker (`automation/`). Schedules use Asia/Kolkata. Workflows: welcome, follower alerts, notification cleanup, daily stats, unread digest, weekly report, monthly report, failure digest. Retries, timeouts, idempotency keys, and failure logs. See `automation/README.md`.

## Project Structure

```
project/
├── frontend/          # React + Vite app
├── backend/           # Express API
├── database/          # schema.sql + seed.sql
├── automation/        # Background jobs
├── docs/              # API, DB, Setup docs
├── .env.example
├── .gitignore
└── README.md
```

## Installation

### Prerequisites
- Node.js 18+
- MySQL 8+
- npm or yarn

### 1. Clone / Download
```bash
cd project
```

### 2. Environment Variables
```bash
cp .env.example .env
# Edit .env with your MySQL credentials and a strong JWT_SECRET
```

### 3. Database Setup
```bash
# Login to MySQL
mysql -u root -p

# Create database and run schema
source database/schema.sql
source database/seed.sql
```

Or from terminal:
```bash
mysql -u root -p < database/schema.sql
mysql -u root -p < database/seed.sql
```

### 4. Backend Setup
```bash
cd backend
npm install
npm run dev
```
Backend runs at `http://localhost:5000`

### 5. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```
Frontend runs at `http://localhost:5173`

### 6. Automation (separate process)
```bash
cd automation
npm install
npm start
```
Schedules run in Asia/Kolkata. Optional manual run: `node index.js run dailyStats`.

## How to Run Locally

1. Start MySQL service
2. Ensure `.env` is configured
3. Run backend: `cd backend && npm run dev`
4. Run frontend: `cd frontend && npm run dev`
5. Open browser → http://localhost:5173

**Demo accounts** (from seed):
- email: `alex@pulse.app` / password: `password123`
- email: `sam@pulse.app` / password: `password123`

## Production Deployment

### Backend
- Set `NODE_ENV=production`
- Use a process manager (PM2)
- Put behind Nginx reverse proxy
- Enable HTTPS
- Use strong JWT_SECRET and restricted DB user

### Frontend
```bash
cd frontend
npm run build
```
Serve the `dist/` folder with Nginx or any static host (Vercel, Netlify, etc.)

### Database
- Use managed MySQL (AWS RDS, PlanetScale, etc.)
- Enable SSL connections
- Regular backups

## API Documentation
See `docs/API.md`

## Database Schema
See `docs/DATABASE.md`

## License
MIT
