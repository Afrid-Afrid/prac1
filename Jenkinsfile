pipeline {
    agent any

    triggers {
        cron('* * * * *')
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Afrid-Afrid/prac1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python app.py &'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t flask-app:v1 .'
            }
        }

        stage('Deploy Swarm') {
            steps {
                sh 'docker service create --name flask-service -p 5000:5000 flask-app:v1'
            }
        }
    }
}