pipeline {
    agent any

    environment {
	    APP_NAME = "laravel-app"
        RELEASE = "1.0.0"
        DOCKER_USER = "titasuddin"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	    //JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")
    }
    
    stages{
        stage('code'){
            steps {
                git url: 'https://github.com/titasuddin/devops_project1.git', branch: 'main'
            }
        }
        
        stage('SonarQube Analysis'){
            steps{
                script {
                   scannerHome = tool 'sonarqube-scanner'
                }
                withSonarQubeEnv('sonarqube-server') {
                   sh "${scannerHome}/bin/sonar-scanner"
                }

            }

        }
        stage("Quality Gate"){
           steps {
               script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token'
                }	
            }

        }

     
        stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}", "-f app1/build/Dockerfile ."
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }
        }    
    }
}
