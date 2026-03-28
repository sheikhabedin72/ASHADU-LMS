# 🛠️ ASHADU-LMS Development Setup Guide

## Table of Contents
1. [System Requirements](#system-requirements)
2. [Environment Setup](#environment-setup)
3. [Backend Configuration](#backend-configuration)
4. [Frontend Configuration](#frontend-configuration)
5. [Database Setup](#database-setup)
6. [Running the Application](#running-the-application)
7. [Troubleshooting](#troubleshooting)

---

## System Requirements

### Hardware
- CPU: Multi-core processor (2+ cores recommended)
- RAM: 8GB minimum (16GB recommended)
- Storage: 20GB free space

### Software
- **Node.js**: v18.0.0 or higher ([Download](https://nodejs.org/))
- **npm**: v9.0.0 or higher (comes with Node.js)
- **PostgreSQL**: v13+ ([Download](https://www.postgresql.org/))
- **Git**: v2.30+ ([Download](https://git-scm.com/))
- **Docker** (Optional, for containerization): v20.10+

### API Keys Required
- **OpenAI API Key**: Sign up at https://platform.openai.com/
- **Optional**: Supabase account for vector DB

---

## Environment Setup

### 1. Install Node.js

#### On Windows
- Download the LTS version from https://nodejs.org/
- Run the installer and follow the prompts
- Verify installation: `node --version` and `npm --version`

#### On macOS
```bash
# Using Homebrew
brew install node

# Verify installation
node --version
npm --version
```

#### On Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install nodejs npm

# Verify installation
node --version
npm --version
```

### 2. Install PostgreSQL

#### On Windows
- Download installer from https://www.postgresql.org/download/windows/
- Run installer and follow the setup wizard
- Remember the password you set for the `postgres` user

#### On macOS
```bash
brew install postgresql@15
brew services start postgresql@15
```

#### On Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install postgresql postgresql-contrib

# Start PostgreSQL
sudo systemctl start postgresql
```

### 3. Verify PostgreSQL Installation
```bash
psql --version
psql -U postgres -c "SELECT version();"
```

---

## Backend Configuration

### 1. Create Backend Directory Structure
```bash
cd ASHADU-LMS
mkdir -p backend
cd backend
```

### 2. Initialize Node Project
```bash
npm init -y
```

### 3. Install Dependencies
```bash
npm install express cors dotenv bcryptjs jsonwebtoken pg prisma @prisma/client
npm install --save-dev nodemon typescript @types/node @types/express
```

### 4. Create Environment File
```bash
# Create .env file
cat > .env << EOF
# Database Configuration
DATABASE_URL=postgresql://postgres:your_password@localhost:5432/ashadu_lms
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=your_password
DB_NAME=ashadu_lms

# Server Configuration
PORT=5000
NODE_ENV=development

# Authentication
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRATION=7d
REFRESH_TOKEN_EXPIRATION=30d

# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-4

# Supabase (Optional for Vector DB)
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key

# Application Settings
LOG_LEVEL=debug
MAX_FILE_UPLOAD_SIZE=52428800
EOF
```

### 5. Create Project Structure
```bash
mkdir -p src/{controllers,services,models,middleware,routes,utils,ai}
mkdir -p tests
mkdir -p scripts
```

### 6. Create Basic Express Server
Create `src/index.ts`:
```typescript
import express from 'express';
import cors from 'cors';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(express.json());

// Health check endpoint
app.get('/api/health', (req, res) => {
  res.json({ status: 'Server is running' });
});

// Start server
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### 7. Update package.json Scripts
```json
{
  "scripts": {
    "dev": "nodemon src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "test": "jest",
    "migrate": "prisma migrate deploy",
    "db:push": "prisma db push"
  }
}
```

---

## Frontend Configuration

### 1. Create Frontend Project with Next.js
```bash
cd ../
npx create-next-app@latest frontend --typescript --tailwind --eslint
cd frontend
```

### 2. Install Additional Dependencies
```bash
npm install axios zustand next-auth dotenv-local
npm install --save-dev @types/react @types/node
```

### 3. Create Environment File
```bash
cat > .env.local << EOF
# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_APP_NAME=ASHADU-LMS

# Authentication
NEXTAUTH_SECRET=your_next_auth_secret_key
NEXTAUTH_URL=http://localhost:3000

# Optional: Analytics
NEXT_PUBLIC_ANALYTICS_ID=
EOF
```

### 4. Create Project Structure
```bash
mkdir -p app/{dashboard,courses,auth,admin}
mkdir -p components/{common,dashboard,courses,auth}
mkdir -p hooks
mkdir -p lib
mkdir -p types
mkdir -p context
mkdir -p public/images
```

### 5. Update next.config.js
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  swcMinify: true,
  images: {
    domains: ['localhost', 'api.example.com'],
  },
};

module.exports = nextConfig;
```

---

## Database Setup

### 1. Create PostgreSQL Database
```bash
# Connect to PostgreSQL
psql -U postgres

# In the PostgreSQL prompt, run:
CREATE DATABASE ashadu_lms;
CREATE USER ashadu_user WITH PASSWORD 'secure_password';
GRANT ALL PRIVILEGES ON DATABASE ashadu_lms TO ashadu_user;

# Exit
\q
```

### 2. Initialize Prisma (Backend)
```bash
cd backend
npx prisma init
```

### 3. Create Prisma Schema
Edit `prisma/schema.prisma`:
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  username String @unique
  password String
  role  String  @default("student")
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}

model Course {
  id    Int     @id @default(autoincrement())
  title String
  description String?
  createdById Int
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

### 4. Run Database Migration
```bash
npx prisma migrate dev --name init
npx prisma generate
```

---

## Running the Application

### Start Backend
```bash
cd backend
npm run dev
# Backend should run on http://localhost:5000
```

### Start Frontend (New Terminal)
```bash
cd frontend
npm run dev
# Frontend should run on http://localhost:3000
```

### Verify Everything Works
- Visit http://localhost:3000 in your browser
- Check http://localhost:5000/api/health for backend status

---

## Troubleshooting

### Common Issues

#### 1. PostgreSQL Connection Error
```
Error: connect ECONNREFUSED 127.0.0.1:5432
```
**Solution**:
```bash
# On macOS
brew services start postgresql@15

# On Linux
sudo systemctl start postgresql

# On Windows
# Open Services (services.msc) and start PostgreSQL
```

#### 2. Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::5000
```
**Solution**:
```bash
# Find and kill process using port 5000
# On Linux/macOS
lsof -i :5000
kill -9 <PID>

# On Windows
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

#### 3. Module Not Found Error
```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### 4. TypeScript Errors
```bash
# Ensure TypeScript is installed
npm install --save-dev typescript ts-node

# Generate TypeScript config
npx tsc --init
```

#### 5. CORS Error
**Add to backend `src/index.ts`**:
```typescript
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true
}));
```

---

## Next Steps

After completing setup:

1. ✅ Create your first API endpoint
2. ✅ Set up database models
3. ✅ Build authentication pages
4. ✅ Create dashboard layout
5. ✅ Integrate AI course authoring

---

## Useful Commands

### Backend
```bash
npm run dev              # Start development server
npm run build            # Build for production
npm test                 # Run tests
npm run db:push          # Sync database
npx prisma studio       # Open Prisma Studio (GUI)
```

### Frontend
```bash
npm run dev              # Start development server
npm run build            # Build for production
npm run lint             # Run ESLint
npm test                 # Run tests
```

---

## Resources

- [Node.js Documentation](https://nodejs.org/docs/)
- [Express.js Guide](https://expressjs.com/)
- [Next.js Documentation](https://nextjs.org/docs)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Prisma ORM Guide](https://www.prisma.io/docs/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

---

## Getting Help

- Check the [README.md](./README.md) for general info
- Review [ARCHITECTURE.md](./ARCHITECTURE.md) for system design
- Check [GitHub Issues](https://github.com/sheikhabedin72/ASHADU-LMS/issues) for known problems
- Ask questions in project discussions
