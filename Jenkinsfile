pipeline {
    agent {
        docker {
            image 'python:3.10'  // or any tag you prefer
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/abhishripathak/Flask-Pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Flask App') {
            steps {
                sh 'nohup python app.py > flask.log 2>&1 &'
            }
        }
    }
}
