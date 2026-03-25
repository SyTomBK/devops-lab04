pipeline {
    agent any

    environment {
        IMAGE_NAME = "lab04-api"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SyTomBK/devops-lab04.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh """
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} -f Lab04.Api/Dockerfile .
                """
            }
        }

        stage('Run Container') {
            steps {
                echo 'Stop old container if exists...'
                sh """
                docker rm -f lab04-container || true
                """

                echo 'Run new container...'
                sh """
                docker run -d --name lab04-container -p 8080:8080 ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }

    }

    post {
        always {
            echo 'Pipeline finished.'
        }

        success {
            echo 'Build SUCCESS'
        }

        failure {
            echo 'Build FAILED'
        }
    }
}