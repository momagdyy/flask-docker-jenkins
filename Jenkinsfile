pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'megzz22/flask-app'
        DOCKER_TAG = "v${BUILD_NUMBER}"
    }

    stages {

        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing to Docker Hub...'
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
                    sh "docker push ${DOCKER_IMAGE}:${DOCKER_TAG}"
                }
            }
        }

    }

    post {
        success {
            echo "Image ${DOCKER_IMAGE}:${DOCKER_TAG} pushed successfully! ✅"
        }
        failure {
            echo 'Pipeline failed! ❌'
        }
    }
}

