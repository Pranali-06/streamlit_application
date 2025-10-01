pipeline {
    agent any

    environment {
        APP_FILE = 'app.py'
        APP_PORT = '8501'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Pranali-06/streamlit_application.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'python3 -m pip install --user -r requirements.txt || python3 -m pip install --user streamlit'
            }
        }

        stage('Test Streamlit Run') {
            steps {
                sh """
                python3 -m streamlit run $APP_FILE --server.headless true --server.port $APP_PORT &
                sleep 10
                pkill -f streamlit || true
                """
            }
        }
    }

    post {
        success {
            echo '✅ Streamlit build and test successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
