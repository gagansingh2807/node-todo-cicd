pipeline {
    agent any
    
    stages {
        stage ("code"){
            steps {
                git url: "https://github.com/gagansingh2807/node-todo-cicd.git", branch: "master"
             }
        }
        stage ("build & test"){
            steps{  
                sh "docker build . -t node-app-test-new"
            }
        }
        stage ("push to Dockerhub"){
            steps{
                withCredentials([usernamePassword(credentialsId: "DockerHub", passwordVariable: "DockerHubPass", usernameVariable: "DockerHubUser")]) {
                    sh 'docker login -u $DockerHubUser -p $DockerHubPass'
                    sh "docker tag node-app-test-new $DockerHubUser/node-app-test-new:latest"
                    sh "docker push $DockerHubUser/node-app-test-new"

                }
            }
        }
        stage ("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
