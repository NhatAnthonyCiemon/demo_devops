# Demo DevOps Project

A full-stack web application demonstrating modern DevOps practices including CI/CD pipelines, containerization with Docker, and automated deployment.

## 📋 Project Overview

This project showcases a complete DevOps workflow with:
- **Frontend**: React + TypeScript application with Vite
- **Backend**: Node.js + Express API with Prisma ORM
- **Database**: PostgreSQL
- **CI/CD**: GitHub Actions for automated building, testing, and deployment
- **Containerization**: Docker & Docker Compose
- **Container Registry**: GitHub Container Registry (GHCR)

## 🛠️ Technology Stack

### Frontend
- React 19
- TypeScript
- Vite
- TailwindCSS
- React Query (TanStack Query)
- React Router
- Framer Motion
- React Hook Form

### Backend
- Node.js
- Express 5
- Prisma ORM
- PostgreSQL
- Passport.js (OAuth authentication)
- JWT Authentication
- Nodemailer

### DevOps Tools
- Docker & Docker Compose
- GitHub Actions
- GitHub Container Registry (GHCR)
- SSH deployment

## 📦 Prerequisites

Before running this project, ensure you have:
- [Docker](https://docs.docker.com/get-docker/) (version 20.10+)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 2.0+)
- [Node.js](https://nodejs.org/) (version 18+ for local development)
- [Git](https://git-scm.com/)

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/NhatAnthonyCiemon/demo_devops.git
cd demo_devops
```

### 2. Configure Environment Variables

Create environment files for each service:

#### Database (.env in db folder)
```bash
mkdir -p db
cat > db/.env << EOF
POSTGRES_USER=postgres
POSTGRES_PASSWORD=your_secure_password
POSTGRES_DB=demo_devops
EOF
```

#### Backend (.env in backend folder)
```bash
mkdir -p backend
cat > backend/.env << EOF
DATABASE_URL=postgresql://postgres:your_secure_password@postgres:5432/demo_devops
JWT_SECRET=your_jwt_secret_key
NODE_ENV=production
BE_PORT=4000
EOF
```

#### Frontend (.env in frontend folder)
```bash
mkdir -p frontend
cat > frontend/.env << EOF
VITE_API_URL=http://localhost:4000
EOF
```

### 3. Run with Docker Compose

```bash
# Pull the latest images from GitHub Container Registry
docker compose pull

# Start all services
docker compose up -d

# View logs
docker compose logs -f
```

The application will be available at:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:4000
- **PostgreSQL**: localhost:5432

### 4. Stop the Application

```bash
docker compose down

# To remove volumes as well
docker compose down -v
```

## 💻 Local Development

### Backend Development

```bash
cd be
npm install
npm run dev
```

### Frontend Development

```bash
cd fe
npm install
npm run dev
```

## 🔄 CI/CD Pipeline

This project uses GitHub Actions for automated CI/CD:

### Continuous Integration (CI)
**File**: `.github/workflows/ci.yml`

- **Trigger**: Push to `main` branch or Pull Requests
- **Jobs**:
  1. Build Backend Docker image
  2. Build Frontend Docker image
  3. Push images to GitHub Container Registry (on main branch only)

### Continuous Deployment (CD)
**File**: `.github/workflows/cd.yml`

- **Trigger**: After successful CI workflow or manual dispatch
- **Jobs**:
  1. Login to production server via SSH
  2. Pull latest Docker images
  3. Run database migrations
  4. Restart services with zero downtime
  5. Clean up old Docker images

## 🔐 Required GitHub Secrets

For CI/CD pipelines to work, configure these secrets in your GitHub repository:

| Secret Name | Description |
|-------------|-------------|
| `TOKEN` | GitHub Personal Access Token with package write permissions |
| `SERVER_IP` | Production server IP address |
| `USER` | SSH username for deployment |
| `SSH_PRIVATE_KEY` | SSH private key for server access |
| `VITE_API_URL` | Backend API URL for frontend builds |

## 📁 Project Structure

```
demo_devops/
├── .github/
│   └── workflows/
│       ├── ci.yml          # CI pipeline
│       └── cd.yml          # CD pipeline
├── be/                     # Backend application
│   ├── src/
│   ├── prisma/            # Database schema and migrations
│   ├── Dockerfile
│   ├── package.json
│   └── app.js
├── fe/                     # Frontend application
│   ├── src/
│   ├── public/
│   ├── Dockerfile
│   ├── package.json
│   └── vite.config.ts
├── docker-compose.yml      # Docker Compose configuration
└── .env.example           # Environment variables template
```

## 🐳 Docker Images

Images are automatically built and published to GitHub Container Registry:

- **Backend**: `ghcr.io/nhatanthonyciemon/demo_devops/demo-backend:latest`
- **Frontend**: `ghcr.io/nhatanthonyciemon/demo_devops/demo-frontend:latest`

## 🔧 Available Scripts

### Backend
- `npm run dev` - Start development server with hot reload
- `npm run build` - Generate Prisma client
- `npm start` - Start production server

### Frontend
- `npm run dev` - Start Vite development server
- `npm run build` - Build for production
- `npm run lint` - Run ESLint
- `npm run preview` - Preview production build

## 📝 Database Management

The project uses Prisma ORM for database management:

```bash
# Generate Prisma Client
cd be
npx prisma generate

# Push schema changes to database
npx prisma db push

# Open Prisma Studio (GUI for database)
npx prisma studio
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This is a demo project for educational purposes.

## 👤 Author

**Thanh Nhat**
- Email: nhatmonsterhack@gmail.com
- GitHub: [@NhatAnthonyCiemon](https://github.com/NhatAnthonyCiemon)

## 🙏 Acknowledgments

This project demonstrates best practices in:
- Modern web application development
- DevOps automation
- Container orchestration
- CI/CD pipeline implementation
- Infrastructure as Code

---

**Note**: This is a demonstration project for learning DevOps practices. For production use, ensure proper security measures, monitoring, and backup strategies are in place.
