@Library('my-shared-library') _

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "megzz22/flask-app:v${BUILD_NUMBER}"
    }

    stages {
        stage('Run Shared Library') {
            steps {
                dockerBuild("${DOCKER_IMAGE}")
            }
        }
    }

    post {
        success {
            echo "Image ${DOCKER_IMAGE} pushed successfully! ✅"
        }
        failure {
            echo 'Pipeline failed! ❌'
        }
    }
}
