pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_NAME = 'nodejsimage' // Name for your Docker image
        DOCKER_IMAGE_TAG = 'girish186/nodejsimage' // Tag for your Docker image
        CONTAINER_PORT = 3000 // Port your Node.js application listens on
        HOST_PORT = 8080 // Port on the host machine to bind to
        GIT_USERNAME = credentials('Girishgit123') // Jenkins credential ID for Git username
        GIT_PASSWORD = credentials('Ramrao@1')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Girishgit123/kubernetes.git' // Your Node.js application repository URL
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${nodejsimage}:${girish186/nodejsimage}") // Build Docker image
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    docker.run("-p ${HOST_PORT}:${CONTAINER_PORT} -d ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}") // Run Docker container
                }
            }
        }
    }
}
