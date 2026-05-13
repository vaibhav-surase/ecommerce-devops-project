pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/vaibhav-surase/ecommerce-devops-project.git'
            }
        }


        stage('Build Frontend') {
            steps {
                sh 'docker build -t vaibhavsurase/frontend:v1 frontend/'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t vaibhavsurase/backend:v1 backend/'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push vaibhavsurase/frontend:v1'
                sh 'docker push vaibhavsurase/backend:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
