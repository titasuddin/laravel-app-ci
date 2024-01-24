pipeline {
    agent any
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/titasuddin/devops_project1.git', branch: 'main'
            }
        }
        stage('Build and Test'){
            steps {
                sh 'docker build -t titasuddin/app1:latest -f app1/build/Dockerfile .'
                
                
            }
        }
        stage('Login and Push Image'){
            steps {
                echo 'logging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'DockerHubPassword', usernameVariable:'DockerHubUsername')]) {
                    sh "docker login -u ${env.DockerHubUsername} -p ${env.DockerHubPassword}"
                    sh "docker push titasuddin/app1:latest"
                }    
            }
        }
    }
}
