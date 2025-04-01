pipeline {
    agent any

    environment {
        IMAGE_NAME = "muruganpm/onlinebookstore"
        CONTAINER_NAME = "onlinebookstore-container"
        HOST_PORT = "8080"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image using multi-stage build..."
                    sh 'docker build -t ${IMAGE_NAME} .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo "Stopping old container if it exists..."
                    sh "docker rm -f ${CONTAINER_NAME} || true"

                    echo "Running new container..."
                    sh "docker run -d -p ${HOST_PORT}:8080 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "✅ App running at http://localhost:${HOST_PORT}/onlinebookstore"
        }
        failure {
            echo "❌ Something went wrong!"
        }
    }
