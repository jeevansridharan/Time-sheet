# Time-sheet Application

A comprehensive time-tracking application built with React frontend and Node.js/Express backend, featuring user authentication, project management, and time entry tracking.

## Features

- **User Authentication**: Secure registration and login with JWT tokens
- **Time Tracking**: Track time entries with start/end times
- **Project Management**: Create and manage projects with hourly rates using Prisma ORM
- **Dashboard**: Visualize time entries with calendar views and statistics
- **Teams & People**: Manage team members and their projects

## Tech Stack

- **Frontend**: React 18 with Vite
- **Backend**: Node.js + Express
- **Database**: SQLite with Prisma ORM (for projects/entries)
- **Authentication**: JWT with bcryptjs
- **Charting**: Chart.js and vis-timeline

## Quick Start

### Installation

```bash
# Install server dependencies
npm install

# Install client dependencies
cd client
npm install
cd ..
```

### Configuration

Create a `.env` file in the root directory:

```env
DATABASE_URL="file:./prisma/prisma/dev.db"
JWT_SECRET="dev-secret-change-in-production"
PORT=3000
```

### Database Setup

```bash
# Generate Prisma client
npm run prisma:generate

# Run migrations (if needed)
npm run prisma:migrate
```

### Build and Run

```bash
# Build the client
cd client
npm run build
cd ..

# Start the server (serves both API and built client)
npm start
```

The application will be available at `http://localhost:3000`

## Development

### Running in Development Mode

```bash
# Terminal 1: Run the server with auto-reload
npm run dev

# Terminal 2: Run the client dev server (optional)
cd client
npm run dev
```

### Running Tests

```bash
npm test
```

## API Endpoints

- `POST /register` - Register a new user
  - Body: `{ email, password, name?, age?, gender?, phone? }`
- `POST /login` - Login with credentials
  - Body: `{ email, password }`
- `GET /me` - Get current user info
  - Headers: `Authorization: Bearer <token>`
- Projects and time entries endpoints (see server/index.js for full API)

## Scripts

- `npm start` - Start the production server
- `npm run dev` - Start server with nodemon
- `npm test` - Run tests
- `npm run create-admin` - Create an admin user
- `npm run prisma:generate` - Generate Prisma client
- `npm run prisma:migrate` - Run database migrations

## Setting an Initial Admin User

You can create an admin user automatically on startup by setting environment variables:

```bash
# Linux/Mac
export ADMIN_EMAIL='admin@example.com'
export ADMIN_PASSWORD='a_strong_password'
export ADMIN_NAME='Admin User'
npm start

# Windows PowerShell
$env:ADMIN_EMAIL = 'admin@example.com'
$env:ADMIN_PASSWORD = 'a_strong_password'
$env:ADMIN_NAME = 'Admin User'
npm start
```

The server will create this user in `server/db.json` if the users array is empty.

## Project Structure

```
.
├── client/              # React frontend
│   ├── src/            # React components
│   └── dist/           # Built frontend (after npm run build)
├── server/             # Express backend
│   ├── index.js        # Main server file
│   ├── db.js           # JSON file database utilities
│   └── __tests__/      # Server tests
├── prisma/             # Prisma schema and database
├── scripts/            # Utility scripts
└── package.json        # Server dependencies
```

## Notes

- Authentication uses a JSON file (`server/db.json`) for user storage
- Projects and time entries use Prisma with SQLite
- For production, consider migrating to PostgreSQL or MySQL
- Change the JWT_SECRET before deploying to production
- The built client is served from the Express server on port 3000
