pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "streamlit-app"
        CONTAINER_NAME = "streamlit_container"
        APP_PORT = "8501"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t streamlit-app ."
            }
        }

        stage('Remove Old Container') {
            steps {
                echo "Removing old container if exists..."
                sh "docker rm -f streamlit_container || true"
            }
        }

        stage('Run Container') {
            steps {
                echo "Running new container..."
                sh docker run -d --name streamlit_container -p 8501:8501 streamlit-app
                    
            
            }
        }
    }
}
