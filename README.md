Project Overview:  
I initiated this project with the goal of deploying a Laravel application using a robust CI/CD pipeline. The entire infrastructure was set up on AWS cloud for scalability and reliability.
![cicd](https://github.com/titasuddin/laravel-app-ci/assets/86006558/eabb28ce-5bb6-4fc3-b7be-9b10e6087455)
GitHub Directory Structure:

Repository 1: https://github.com/titasuddin/laravel-app-ci.git

app  
&nbsp;&nbsp;&nbsp;src  
&nbsp;&nbsp;&nbsp;build  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Dockerfile  
infra  
-README.md  
-Jenkinsfile  
-README.md

Repository 2: https://github.com/titasuddin/laravel-app-cd.git

-Jenkinsfile  
-README.md  
-deployment.yaml  
-service.yaml


Infrastructure Details:  

EKS Bootstrap Server  
Jenkins Server  
SonarQube Server  
EKS Cluster  
&nbsp;&nbsp;1 Master Node  
&nbsp;&nbsp;2 Worker Nodes

Technologies/Tools Used:

GitHub: Version control and collaboration.  
Jenkins: Automation server for CI/CD pipelines.  
SonarQube: Ensuring code quality and security.
Docker & DockerHub: Containerization for consistent deployment.  
Trivy: Vulnerability scanner for Docker containers  
ArgoCD: GitOps continuous delivery tool for Kubernetes  
EKS Kubernetes Cluster: Managed Kubernetes service for container orchestration.  

