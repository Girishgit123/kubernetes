pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'myimage'
        DOCKER_REGISTRY = 'girish'
        DOCKER_CREDENTIALS_ID = 'dockerid'
    }


    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository with specified credentials
                git branch: 'main', credentialsId: 'ca7bb99a-807f-4305-af7a-4b4aa6ff72bb', url: 'https://github.com/Girishgit123/kubernetes.git'   
            }
        }
    }
}


         stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t myimage ."
            }
        }
            stage(push to dockerhub){
                steps{
                    echo "Push the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerid",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag myimage ${env.dockerHubUser}/myimage:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/myimage:latest"
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
