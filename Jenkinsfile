pipeline {
    agent any

    environment {
        APP_NAME = "flask-app"
        IMAGE_NAME = "flask-app-image"
        CONTAINER_NAME = "flask-container"
        PORT = "5000"
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📥 Checking out code from GitHub'
                git branch: 'main', url: 'https://github.com/abhishripathak/Flask-Pipeline.git'
  // Update if using a different repo
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📦 Installing Python dependencies'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running tests (if any)'
                // Replace with pytest/unittest if you have tests
                sh 'echo "No tests defined yet!"'
            }
        }

        stage('Docker Build') {
            steps {
                echo '🐳 Building Docker image'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Docker Run') {
            steps {
                echo '🚀 Running Docker container'
                sh '''
                    docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_NAME
                    sleep 5
                    curl http://localhost:$PORT
                '''
            }
        }
    }

    post {
        always {
            echo '🧹 Cleaning up...'
            sh 'docker stop $CONTAINER_NAME || true'
            sh 'docker rm $CONTAINER_NAME || true'
        }

        success {
            echo '✅ Pipeline completed successfully!'
        }

        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
