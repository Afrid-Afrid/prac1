pipeline {
    agent any

    triggers {
        cron('* * * * *')
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh './venv/bin/python app.py &'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t flask-app:v1 .'
            }
        }

        stage('Deploy Swarm') {
            steps {
                sh 'docker service rm flask-service || true'
                sh 'docker service create --name flask-service -p 5000:5000 flask-app:v1'
            }
        }
    }
}