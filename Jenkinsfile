pipeline {
    agent any

    environment {
	APP_NAME = "laravel-app"
        RELEASE = "1.0.0"
        DOCKER_USER = "titasuddin"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
	JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")
    }
    
    stages{
        stage('checkout from SCM'){
            steps {
                git url: 'https://github.com/titasuddin/devops_project1.git', branch: 'main'
            }
        }
	stage("Unit test") {
            steps {
		sh "pwd"
                dir('app/src') {
                sh "pwd"
		sh 'rm -rf vendor composer.lock
		sh 'cp .env.example .env'
		sh 'php artisan key:generate'
		sh 'composer install'
		sh 'php artisan test'
		}
	    }
    }
    sh "pwd"
                sh 'php artisan test'
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
                        docker_image = docker.build "${IMAGE_NAME}", "-f app/build/Dockerfile ."
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }
        }

        stage("Trivy Scan") {
           steps {
               script {
	            sh ('docker run -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image titasuddin/laravel-app:latest --no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table')
               }
            }
        }

	stage("Trigger CD Pipeline") {
            steps {
                script {
                    sh "curl -v -k --user admin:${JENKINS_API_TOKEN} -X POST -H 'cache-control: no-cache' -H 'content-type: application/x-www-form-urlencoded' --data 'IMAGE_TAG=${IMAGE_TAG}' '13.200.82.127:8080/job/laravel-app-cd/buildWithParameters?token=gitops-token'"
                }
            }
       }
    }
    
}
