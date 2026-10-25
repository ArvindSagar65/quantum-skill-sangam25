# Armed Forces Welfare Management System

A full-stack platform that brings welfare services, emergency support, community resources, and grievance handling together for armed forces personnel and their families.

The repository contains a Next.js frontend and an Express.js backend. The backend stores application data in MongoDB, uses Firebase Admin SDK for authentication support, and provides real-time communication through Socket.IO.

## Features

- **Welfare schemes**: Browse schemes, check eligibility, submit applications, and track status.
- **Emergency network**: Share emergency alerts and connect users with responders and support services.
- **Resource marketplace**: Exchange books, equipment, housing, and other community resources.
- **Grievance redressal**: Submit, prioritize, track, and resolve complaints through a structured workflow.
- **User and role management**: Support for administrators, officers, and family members.
- **Real-time updates**: Socket.IO notifications and marketplace messaging.
- **Secure API foundation**: Firebase authentication support, request validation, rate limiting, Helmet, CORS, and centralized error handling.
- **Operations tooling**: Swagger API documentation, database indexes, seed data, backups, logging, scheduled jobs, Docker, and PM2 support.

## Technology Stack

| Layer | Technologies |
| --- | --- |
| Frontend | Next.js 15, React 19, TypeScript, Tailwind CSS, Radix UI, Framer Motion |
| Backend | Node.js, Express, Socket.IO, Swagger/OpenAPI |
| Data and services | MongoDB, Mongoose, Firebase Admin SDK, Nodemailer, Twilio |
| Testing and quality | Jest, Supertest, MongoDB Memory Server, ESLint, Prettier |

## Repository Structure

```text
.
├── backend/             # Express API, models, routes, services, tests, and scripts
├── frontend/            # Next.js application and reusable UI components
├── backend/docker-compose.yml
└── README.md
```

Important backend directories:

```text
backend/
├── config/              # Database, Firebase, logger, and workflow configuration
├── middleware/          # Authentication, validation, uploads, and error handling
├── models/              # Mongoose schemas
├── routes/              # Auth, dashboard, welfare, emergency, marketplace, and grievance APIs
├── scripts/             # Seeding, indexes, and backup utilities
├── utils/               # Notifications, scheduling, sockets, and database helpers
└── __tests__/           # Health, unit, integration, and performance tests
```

## Prerequisites

- Node.js 16 or later
- npm 8 or later
- MongoDB 5 or later, locally or through Docker
- A Firebase project and Firebase Admin SDK credentials for authenticated backend features

## Getting Started

### 1. Install dependencies

Run each application from its own directory:

```bash
cd backend
npm install

cd ../frontend
npm install
```

### 2. Configure the backend

Create a `backend/.env` file and provide the values required by the deployment environment, including:

- MongoDB connection details
- Server port and environment
- Firebase Admin SDK credentials
- Email and SMS provider credentials, when those services are enabled
- Any application secrets used by the backend

The backend listens on port `3001` by default. Make sure MongoDB is running before starting it.

### 3. Start the backend

```bash
cd backend
npm run dev
```

For a production-style start:

```bash
npm start
```

The backend provides:

- API root: `http://localhost:3001/`
- Health check: `http://localhost:3001/health`
- Swagger UI: `http://localhost:3001/api/docs`
- Swagger JSON: `http://localhost:3001/api/docs.json`

### 4. Start the frontend

In a second terminal:

```bash
cd frontend
npm run dev
```

Open `http://localhost:3000` in a browser. The backend CORS configuration also permits the frontend on port `5173` for alternate local development setups.

## Database Utilities

Run these commands from `backend/`:

```bash
# Create or refresh database indexes
npm run indexes

# Load sample data
npm run seed

# Create, restore, or list backups
npm run backup create
npm run backup restore <backup-path>
npm run backup list
```

## Testing and Code Quality

Run these commands from `backend/`:

```bash
npm test                 # Run the complete Jest suite
npm run test:unit        # Run unit tests
npm run test:integration # Run integration tests
npm run test:health      # Check the running health endpoint
npm run test:coverage    # Generate a coverage report
npm run lint             # Run ESLint
npm run format           # Format backend files with Prettier
```

Run the frontend production checks from `frontend/`:

```bash
npm run build
npm start
```

## Docker and Process Management

The backend includes Docker configuration for local or deployment environments:

```bash
cd backend
docker compose up -d
```

For a PM2-managed deployment, use the included ecosystem file:

```bash
cd backend
pm2 start ecosystem.config.js --env production
```

## API Areas

The backend exposes route groups for:

- `/api/auth` - Authentication and profiles
- `/api/users` - User management
- `/api/dashboard` - Dashboard data
- `/api/welfare` - Welfare schemes and applications
- `/api/emergency` - Emergency alerts and responses
- `/api/marketplace` - Community resource listings and inquiries
- `/api/grievance` - Grievance tickets and resolution workflows

See the Swagger UI at `/api/docs` for request and response schemas.

## Authentication

Protected API requests use a Firebase ID token in the authorization header:

```http
Authorization: Bearer <firebase-id-token>
```

Access is controlled by user roles such as Admin, Officer, and Family Member. Keep credentials and service-account files out of source control.

## License

This project is licensed under the MIT License.
