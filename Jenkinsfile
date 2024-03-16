pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE_NAME = 'nodejsimage' // Name for your Docker image
        DOCKER_IMAGE_TAG = 'girish186/nodejsimage' // Tag for your Docker image
        CONTAINER_PORT = 3000 // Port your Node.js application listens on
        HOST_PORT = 8080 // Port on the host machine to bind to
       
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Use withCredentials to bind global Git credentials
                withCredentials([usernamePassword(credentialsId: 'gitglobal', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    // Inside this block, GIT_USERNAME and GIT_PASSWORD environment variables will be available
                    git credentialsId: 'gitglobal', url: 'https://github.com/Girishgit123/kubernetes.git', branch: 'main'
                }
            }
        }
        
        // Add more stages as needed
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
