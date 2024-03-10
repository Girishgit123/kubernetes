pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'myimage'
        DOCKER_REGISTRY = 'girish'
        DOCKER_CREDENTIALS_ID = '9058c779-e5ac-4571-affb-b48c1a893dce'
        GIT_CREDENTIAL_ID = 'ca7bb99a-807f-4305-af7a-4b4aa6ff72bb'
    }


    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository with specified credentials
                git credentialsId: 'GIT_CREDENTIAL_ID' , url: 'https://github.com/Girishgit123/kubernetes.git'
            }
        }
    }
}

    

        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

    

        stage('Package') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Publish') {
            steps {
                script {
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS_ID) {
                        docker.image(DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).run('-p 3000:3000 -d')
                }
            }
        }
