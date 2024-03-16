pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "nodejsimage"
        DOCKER_REGISTRY_CREDENTIALS = 'dockergloabal'
    }

    stages {
        
    stage('Checkout from Git') {
            steps {
                git credentialsId: 'gitglobal', url: 'https://github.com/Girishgit123/kubernetes.git'
            }
    }

        stage('Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Test') {
            steps {
                // Add your test commands here
                sh 'npm install'
                sh 'npm test'
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    withCredentials([string(credentialsId: "${DOCKER_REGISTRY_CREDENTIALS}", variable: 'DOCKER_PASSWORD')]) {
                        docker.withRegistry('https://your.docker.registry', 'docker-registry-credentials') {
                            docker.image("${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // If needed, deploy your Docker container here
                sh 'docker run -d -p 8080:8080 ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}'
            }
        }
    }
}
