pipeline {
    agent any

    environment {
        IMAGE_NAME = 'node-status-api'
        CONTAINER_NAME = 'node-status-container'
        PORT = '3000'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building the Docker image...'
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo 'Deploying the application...'
                // Stop and remove the old container if it exists
                bat """
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}
                """
            }
        }
        
        stage('Verify Deployment') {
            steps {
                echo "Application successfully deployed and exposed on port ${PORT}."
            }
        }
    }
}