pipeline {
    agent {
        docker {
            image 'docker:20.10' 
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t streamlit-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8501:8501 --name streamlit_container streamlit-app'
            }
        }
    }
}
