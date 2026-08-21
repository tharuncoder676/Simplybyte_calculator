pipeline {
    agent any

    environment {
        // Name your container and image
        IMAGE_NAME = "calculator-app"
        CONTAINER_NAME = "calculator-running"
        PORT = "5000"
    }

    stages {
        stage('Pull Code') {
            steps {
                checkout scm
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    // Stops and removes the old calculator container if it exists
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Build New Image') {
            steps {
                // Builds a fresh image from your Dockerfile
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy Live') {
            steps {
                // Runs the new container detached (-d) so it stays live
                sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest"
            }
        }
    }
}
