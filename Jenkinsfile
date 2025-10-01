pipeline {
    agent any

    environment {
        IMAGE_NAME = 'streamlit_app'        
        CONTAINER_NAME = 'streamlit_container'
        APP_PORT = '8501'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'master', url: 'https://github.com/Pranali-06/streamlit_application.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t streamlit_app ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running Docker container...'
                sh """ 
                docker rm -f streamlit_container || true
                sh docker run -d --name streamlit_container -p 8501:8501 streamlit_app 
                """
            }
        }
    }

    post {
        success {
            echo "Docker build and container run successful!"
            echo "Access the app at http://54.234.8.163:8501"
        }
        failure {
            echo '❌ Build or container run failed. Check console output.'
        }
    }
}
