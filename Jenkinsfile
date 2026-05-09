pipeline {
    agent any

    environment {
        FRONTEND_IMAGE="mern-frontend:jenkins"
        BACKEND_IMAGE="mern-backend:jenkins"
        MONGO_URI = credentials('mongo-uri')
        PORT = credentials('app-port')
    }

    stages {
        stage('Checkout Code'){
            steps {
                git url: 'https://github.com/TeMPesT969/Taskmanager-devops-trial', branch: 'main'
            }
        }

        stage('Prepare .env'){
            steps {
                sh '''
                mkdir -p server
                cat > server/.env <<EOF
                PORT=$PORT
                MONGO_URI=$MONGO_URI
                EOF
                    '''
            }
        }

        stage('Build Docker Images') {
            steps {
                sh '''
                echo "building backend image..."
                docker build -t $BACKEND_IMAGE ./server

                echo "building frontend image..."
                docker build -t $FRONTEND_IMAGE ./client --build-arg VITE_API_URL="http://localhost:5000/api"

                '''
            }
        }

        stage('Run with docker compose'){
            steps {
                sh '''
                echo "Starting MERN app with docker compose..."
                docker compose up -d --no-build

                echo "Showing running containers"
                docker ps

                '''
            }
        }
    }
}