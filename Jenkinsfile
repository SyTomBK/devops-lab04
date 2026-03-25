pipeline {
    agent any

    environment {
        IMAGE_NAME = "lab04-api"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Debug') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -f Lab04.Api/Dockerfile .
                """
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker rm -f lab04-container || true
                docker run -d --name lab04-container -p 8080:8080 ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}