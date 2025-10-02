pipeline {
    agent any

    environment {
        IMAGE_NAME = "streamlit_app"
        CONTAINER_NAME = "streamlit_container"
        APP_PORT = "8501"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling source code from GitHub"
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh """
                    docker build -t streamlit_app .
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running container..."
                sh """
                    docker rm -f streamlit_container || true
                    docker run -d --name streamlit_container -p 8501:8501 streamlit_app
                """
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
            
        }
        
    
    }
}
