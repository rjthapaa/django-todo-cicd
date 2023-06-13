pipeline {
    agent { label "jenkins agent" }
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/rjthapaa/django-todo-cicd.git", branch: "develop"
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build . -t rjthapaa/django-app"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push rjthapaa/django:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
