pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'kubernetes' // Name of your Docker image
        CONTAINER_NAME = 'dreamy_hypatia' // Name of your Docker container
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Install dependencies and build your Node.js application
                    sh 'npm install'
                    sh 'npm run build' // Modify this command according to your build process
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Build Docker image
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Docker Run') {
            steps {
                script {
                    // Run Docker container
                    docker.image(env.DOCKER_IMAGE).run("--name ${env.CONTAINER_NAME} -d -p 3000:3000") // Modify the port mapping as needed
                }
            }
        }

        stage('Test') {
            steps {
                // Run tests if needed
            }
        }

        stage('Deploy') {
            steps {
                // Perform any additional deployment steps here
            }
        }
    }

    post {
        always {

            // Clean up
            script {
                docker.image(env.DOCKER_IMAGE).stop()
                docker.image(env.DOCKER_IMAGE).remove()
            }
        }
    }
}

