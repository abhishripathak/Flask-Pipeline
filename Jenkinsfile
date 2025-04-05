pipeline {
    agent {
        docker {
            image 'python:3.10'
        }
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/abhishripathak/Flask-Pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Flask App (test only)') {
            steps {
                sh 'python app.py & sleep 5'
                sh 'curl http://localhost:5000'
            }
        }

        stage('Docker Build & Tag') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Docker Run Test') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask_container flask-app'
                sh 'sleep 5 && curl http://localhost:5000'
                sh 'docker stop flask_container && docker rm flask_container'
            }
        }
    }
}
