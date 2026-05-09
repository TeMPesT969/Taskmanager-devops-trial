# 📋 Task Manager — MERN DevOps Project

A full-stack Task Manager application built with the MERN stack, containerized with Docker, and automated with a CI/CD pipeline using Jenkins and GitHub Actions. Built as a hands-on learning project covering real-world DevOps practices.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React (Vite) |
| Backend | Node.js + Express |
| Database | MongoDB |
| Containerization | Docker + Docker Compose |
| CI/CD | Jenkins + GitHub Actions |
| Cloud | AWS EC2 (deployment target) |
| Code Quality | ESLint + Prettier |

---

## 📁 Project Structure

```
devops-youtube-course-2025/
├── .github/
│   └── workflows/
│       └── ci.yml           # GitHub Actions CI pipeline
├── client/                  # React frontend (Vite)
│   ├── src/
│   ├── public/
│   ├── Dockerfile
│   ├── .env.example
│   └── eslint.config.js
├── server/                  # Node.js + Express backend
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── Dockerfile
│   └── .env.example
├── docker-compose.yml       # Multi-container setup
├── Jenkinsfile              # Jenkins pipeline definition
└── README.md
```

---

## ⚙️ CI/CD Pipeline

### GitHub Actions (`ci.yml`)
Triggers on push or pull request to `main` and `dev` branches:
- Checks out the repository
- Sets up Node.js
- Installs dependencies
- Runs linting

### Jenkins Pipeline (`Jenkinsfile`)
- Checks out code from GitHub
- Generates `.env` file from Jenkins credentials
- Builds Docker images for frontend and backend
- Runs the full stack using Docker Compose

---

## 🚀 Getting Started Locally

### Prerequisites
- [Docker](https://www.docker.com/) & Docker Compose
- [Node.js](https://nodejs.org/) (for local dev without Docker)

### 1. Clone the repository

```bash
git clone https://github.com/TeMPesT969/Taskmanager-devops-trial.git
cd Taskmanager-devops-trial
```

### 2. Set up environment variables

```bash
# Backend
cp server/.env.example server/.env

# Frontend
cp client/.env.example client/.env
```

Edit the `.env` files with your values:

```dotenv
# server/.env
PORT=5000
MONGO_URI=mongodb://mongo:27017/taskdb

# client/.env
VITE_API_URL=http://localhost:5000/api
```

### 3. Run with Docker Compose

```bash
docker compose up -d
```

| Service | URL |
|---|---|
| Frontend | http://localhost:5173 |
| Backend API | http://localhost:5000/api |
| MongoDB | mongodb://localhost:27017 |

### 4. Stop the app

```bash
docker compose down
```

---

## ☁️ Deploying to AWS EC2

1. Launch an EC2 instance (Ubuntu, t2.micro for free tier)
2. Open ports `5173` and `5000` in the Security Group
3. SSH into the instance and install Docker:

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker ubuntu
```

4. Clone the repo and follow the local setup steps above
5. Access the app at `http://<your-ec2-public-ip>:5173`

---

## 🧠 What I Learned

This project was built to learn and practice:

- **Docker** — Writing Dockerfiles, multi-stage builds, Docker Compose for multi-container apps
- **Jenkins** — Setting up pipelines, using credentials, automating build and deploy stages
- **GitHub Actions** — Writing CI workflows triggered on push/PR
- **AWS EC2** — Launching instances, configuring security groups, deploying containerized apps
- **ESLint + Prettier** — Code quality and formatting in a real project
- **Git best practices** — `.gitignore`, environment variable management, branch strategy

---

## 📝 Environment Variables Reference

| Variable | Description | Example |
|---|---|---|
| `PORT` | Backend server port | `5000` |
| `MONGO_URI` | MongoDB connection string | `mongodb://mongo:27017/taskdb` |
| `VITE_API_URL` | Frontend API base URL | `http://localhost:5000/api` |

> ⚠️ Never commit `.env` files. Use `.env.example` as a template.

---

## 📄 License

This project is for educational purposes.