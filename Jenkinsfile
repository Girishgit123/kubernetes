pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git branch: 'main', credentialsId: 'ca7bb99a-807f-4305-af7a-4b4aa6ff72bb', url: 'https://github.com/Girishgit123/kubernetes.git'
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t myimage ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerid",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag myimage ${env.dockerHubUser}/myimage:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/myimage:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                docker.image(DOCKER_IMAGE).run('-p 3000:3000 -d')
                
            }
        }
    }
}


