# Attendance Management System (MERN)

Generic attendance system for **School / Office / Coaching** — Web app with MERN stack.

Features: login & roles (admin/teacher/student), groups (class/department/batch), manual marking, QR self check-in with rotating token, leaves, reports + defaulter list + CSV export.

## Structure
```
server/ — Express + Mongoose API
client/ — React + Vite frontend
```

## Quick start

### 1. Backend
```powershell
cd server
Copy-Item .env.example .env
# edit .env -> MONGO_URI, JWT_SECRET
npm install
npm run dev
# optional seed demo data:
# npm run seed
```
API: http://localhost:5000, health: `/api/health`

Seed users (password `password123`):
- admin@demo.com (admin)
- teacher@demo.com (teacher)
- student1@demo.com … student8@demo.com

### 2. Frontend
```powershell
cd client
npm install
# optional: set VITE_API_URL=http://localhost:5000/api in .env, else uses /api proxy
npm run dev
```
App: http://localhost:5173

### 3. QR flow
1. Teacher: Mark page → Load group/date → Open Live QR
2. Student: open Check-in link (or `/check-in`), enter token or scan QR → present marked
3. Token rotates every 60s (`QR_ROTATE_SECONDS` in server .env)

## API summary
- `POST /api/auth/register` {name,email,password,orgName,orgType}
- `POST /api/auth/login`
- `CRUD /api/groups`, `GET/POST /api/orgs/users`
- `POST /api/sessions`, `POST /api/sessions/:id/qr-rotate`, `POST /api/sessions/:id/check-in`, `GET /api/sessions/:id/qr.png`
- `POST /api/attendance/bulk`, `GET /api/attendance/mine`
- `CRUD /api/leaves`
- `GET /api/reports/summary?groupId`, `/defaulter?groupId&threshold=75`, `/export.csv?groupId`
