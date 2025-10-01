pipeline {
    agent any

    environment {
        VENV = "venv"
        APP_PORT = "8501"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python virtual environment and installing dependencies...'
                sh '''
                  python3 -m venv ${VENV}
                  . ${VENV}/bin/activate
                  pip install --upgrade pip
                  pip install -r requirements.txt
                '''
            }
        }

        stage('Run Streamlit App') {
            steps {
                echo 'Running Streamlit app on port ${APP_PORT}...'
                sh '''
                  . ${VENV}/bin/activate
                  # Kill any existing Streamlit process
                  pkill -f "streamlit run" || true
                  nohup streamlit run app.py --server.port ${APP_PORT} --server.headless true > streamlit.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo 'Streamlit app deployed successfully!'
        }
        failure {
            echo 'Build failed! Check logs for errors.'
        }
    }
}
