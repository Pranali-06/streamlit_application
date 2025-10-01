pipeline {
    agent any

    environment {
        VENV = 'venv'
        APP_FILE = 'app.py'  // your main Streamlit file
        APP_PORT = '8501'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'master', url: 'https://github.com/Pranali-06/streamlit_application.git'
            }
        }

        stage('Check Python Version') {
            steps {
                sh 'python3 --version || python --version'
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python virtual environment...'
                sh 'python3 -m venv $VENV || python -m venv $VENV'
                sh '. $VENV/bin/activate && pip install --upgrade pip'
                sh '. $VENV/bin/activate && pip install -r requirements.txt || pip install streamlit'
            }
        }

        stage('Test Streamlit Run') {
            steps {
                echo 'Testing Streamlit app...'
                sh """
                . $VENV/bin/activate
                streamlit run $APP_FILE --server.headless true --server.port $APP_PORT &
                sleep 10
                pkill -f streamlit || true
                """
            }
        }
    }

    post {
        success {
            echo 'Build and Streamlit test successful!'
        }
        failure {
            echo 'Build failed! Check console logs for details.'
        }
    }
}
