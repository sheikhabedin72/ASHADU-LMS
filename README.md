# 🎓 ASHADU-LMS: AI-Powered Learning Management System

![Status](https://img.shields.io/badge/status-active-brightgreen) ![License](https://img.shields.io/badge/license-MIT-blue) ![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)

## 📖 Overview

**ASHADU-LMS** is a next-generation Learning Management System powered by AI, designed to revolutionize how educators create courses and how students learn. The platform leverages **LangChain**, **OpenAI**, and **RAG (Retrieval-Augmented Generation)** to provide intelligent course authoring, personalized learning paths, and an AI tutor system.

### Key Features
- ✨ **AI Course Authoring Agent**: Automatically generate courses from simple inputs
- 🎯 **Adaptive Learning**: Personalized learning paths based on student performance
- 🤖 **AI Tutor**: Real-time question answering and Socratic learning support
- 📊 **Advanced Analytics**: Student performance tracking and at-risk learner detection
- 🔐 **Role-Based Access Control**: Secure multi-role system (Student, Teacher, Admin)
- 📱 **Responsive Design**: Works seamlessly on desktop and mobile devices

---

## 🚀 Quick Start

### Prerequisites
- **Node.js** v18+ ([Download](https://nodejs.org/))
- **PostgreSQL** 13+ ([Download](https://www.postgresql.org/))
- **npm** or **yarn** package manager
- **OpenAI API Key** ([Get one here](https://platform.openai.com/))

### Installation

#### 1. Clone the Repository
```bash
git clone https://github.com/sheikhabedin72/ASHADU-LMS.git
cd ASHADU-LMS
```

#### 2. Backend Setup
```bash
cd backend
npm install
cp .env.example .env

# Configure your .env file
# DATABASE_URL=postgresql://user:password@localhost:5432/ashadu_lms
# OPENAI_API_KEY=your_api_key_here
# JWT_SECRET=your_secret_key

npm run migrate  # Run database migrations
npm run dev     # Start development server
```

#### 3. Frontend Setup
```bash
cd ../frontend
npm install
cp .env.example .env

# Configure your .env file
# NEXT_PUBLIC_API_URL=http://localhost:5000

npm run dev  # Start development server
```

#### 4. Access the Application
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000
- **API Documentation**: http://localhost:5000/api-docs

---

## 📁 Project Structure

```
ASHADU-LMS/
├── backend/                    # Express.js backend
│   ├── src/
│   │   ├── controllers/        # Request handlers
│   │   ├── services/           # Business logic
│   │   ├── models/             # Database models
│   │   ├── middleware/         # Express middleware
│   │   ├── routes/             # API routes
│   │   ├── utils/              # Utility functions
│   │   └── ai/                 # AI/LangChain integration
│   ├── tests/                  # Unit and integration tests
│   ├── .env.example            # Environment variables template
│   └── package.json
├── frontend/                   # Next.js frontend
│   ├── app/                    # Next.js app directory
│   │   ├── dashboard/          # User dashboards
│   │   ├── courses/            # Course pages
│   │   ├── auth/               # Authentication pages
│   │   └── admin/              # Admin pages
│   ├── components/             # React components
│   ├── hooks/                  # Custom React hooks
│   ├── lib/                    # Utility libraries
│   ├── public/                 # Static assets
│   └── package.json
├── DATABASE_SCHEMA.md          # PostgreSQL schema design
├── ARCHITECTURE.md             # System architecture documentation
├── DEVELOPMENT_GUIDE.md        # Developer setup guide
├── API_DOCUMENTATION.md        # API endpoints reference
└── README.md                   # This file
```

---

## 🎯 Development Phases

### Phase 1: Foundation (Weeks 1-3)
- [ ] Project setup and environment configuration
- [ ] Database schema implementation
- [ ] Backend API foundation

### Phase 2: Core Features (Weeks 4-6)
- [ ] User authentication system
- [ ] Role-based access control
- [ ] Frontend setup with Next.js
- [ ] User management API

### Phase 3: AI Integration (Weeks 7-9)
- [ ] LangChain integration
- [ ] AI course authoring agent
- [ ] RAG implementation
- [ ] Course creation UI

### Phase 4: Advanced Features (Weeks 10-12)
- [ ] Student learning experience
- [ ] Adaptive learning algorithms
- [ ] AI tutor and Q&A system
- [ ] Admin dashboard

### Phase 5: Production (Weeks 13-14)
- [ ] Testing and QA
- [ ] Production deployment
- [ ] Monitoring and optimization

---

## 🔧 Configuration

### Environment Variables

**Backend (.env)**
```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/ashadu_lms

# Authentication
JWT_SECRET=your_secret_key_here
JWT_EXPIRATION=7d

# OpenAI
OPENAI_API_KEY=your_api_key_here

# Server
PORT=5000
NODE_ENV=development
```

**Frontend (.env.local)**
```env
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_APP_NAME=ASHADU-LMS
```

---

## 📚 API Documentation

### Authentication
```bash
POST   /api/auth/register          # Register new user
POST   /api/auth/login             # Login user
POST   /api/auth/logout            # Logout user
POST   /api/auth/refresh-token     # Refresh JWT token
```

### Users
```bash
GET    /api/users/:id              # Get user profile
PUT    /api/users/:id              # Update user profile
GET    /api/users                  # List users (admin only)
DELETE /api/users/:id              # Delete user (admin only)
```

### Courses
```bash
GET    /api/courses                # List all courses
POST   /api/courses                # Create new course
GET    /api/courses/:id            # Get course details
PUT    /api/courses/:id            # Update course
DELETE /api/courses/:id            # Delete course
```

### AI Course Authoring
```bash
POST   /api/ai/generate-course     # Generate course from input
POST   /api/ai/generate-syllabus   # Generate course syllabus
POST   /api/ai/generate-lessons    # Generate lessons
POST   /api/ai/generate-quiz       # Generate quiz for lesson
```

For complete API documentation, see [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)

---

## 🧪 Testing

### Run Tests
```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd ../frontend
npm test
```

### Test Coverage
```bash
npm run test:coverage
```

---

## 🚢 Deployment

### Deploy to Production

#### Backend (Railway)
```bash
# Install Railway CLI
npm i -g @railway/cli

# Login to Railway
railway login

# Deploy
railway up
```

#### Frontend (Vercel)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Or deploy via GitHub
# - Connect GitHub repo to Vercel
# - Enable automatic deployments on push
```

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Code Standards
- Follow ESLint configuration
- Write meaningful commit messages
- Add tests for new features
- Update documentation as needed

---

## 📖 Documentation

- [Architecture Guide](./ARCHITECTURE.md) - System architecture and design
- [Database Schema](./DATABASE_SCHEMA.md) - Database design and relationships
- [API Documentation](./API_DOCUMENTATION.md) - Complete API reference
- [Development Guide](./DEVELOPMENT_GUIDE.md) - Developer setup and workflow
- [GitHub Issues](https://github.com/sheikhabedin72/ASHADU-LMS/issues) - Task tracking

---

## 📊 Project Status

| Phase | Status | Completion |
|-------|--------|-----------|
| Phase 1: Foundation | ⏳ Planned | 0% |
| Phase 2: Core Features | ⏳ Planned | 0% |
| Phase 3: AI Integration | ⏳ Planned | 0% |
| Phase 4: Advanced Features | ⏳ Planned | 0% |
| Phase 5: Production | ⏳ Planned | 0% |

---

## 🐛 Bug Reports & Feature Requests

Found a bug? Have an idea? [Open an issue](https://github.com/sheikhabedin72/ASHADU-LMS/issues/new)

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

---

## 👨‍💻 Author

**Sheikh Abedin**
- GitHub: [@sheikhabedin72](https://github.com/sheikhabedin72)

---

## 🙏 Acknowledgments

- [LangChain](https://www.langchain.com/) for AI framework
- [OpenAI](https://openai.com/) for LLM capabilities
- [Next.js](https://nextjs.org/) and [Express.js](https://expressjs.com/) for framework
- The open-source community for inspiration and tools

---

## 📞 Support

Need help? 
- 📧 Email: support@ashadu-lms.com
- 💬 Discord: [Join our community](#)
- 📖 Docs: [Read the documentation](#)

---

**Happy Learning! 🚀**
