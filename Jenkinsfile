// pipeline to build the terraform infrastucture on both AWS and EKS..

pipeline {
    agent any

    environment {//needs to be changed
        //AWS_ACCESS_KEY_ID = credentials('aws_cred')
        //AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        //AWS_DEFAULT_REGION = "us-east-1"
        //ECR_REPOSITORY = "1410-8352-5350.dkr.ecr.us-east-1.amazonaws.com/flask-app"
        //DOCKER_CREDS = credentials('dockerhub')
        //DOCKER_CREDS_USR = credentials('dockerhub').USR
        //DOCKER_CREDS_PSW = credentials('dockerhub').PSW
        DOCKER_REPO = "abdelaziz20598/"
        //GIT_CREDS = credentials('github')
        GIT_REPO_URL = "https://github.com/Abdelaziz20598/DEPI_Final_Project"
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                //git branch: 'master', url: "${GIT_REPO_URL}"
                sh 'git clone "https://github.com/Abdelaziz20598/DEPI_Final_Project.git"'
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', 
                        usernameVariable: 'DOCKER_USERNAME', 
                        passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Log into Docker Hub
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    }
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                dir('./DEPI_Final_Project/App/') {
                    script {
                        sh 'pwd ; ls'
                        sh 'docker build -t ${DOCKER_REPO}my-app .'
                        //sh "docker tag my-app ${ECR_REPOSITORY}:latest"
                        //sh "docker tag my-app ${DOCKER_REPO}"
                        sh 'docker push ${DOCKER_REPO}my-app'
                        
                    }
                }
            }
        }

        stage('Initialize Terraform') {
            steps {
                dir('./terraform') {
                    script {
                        sh 'terraform init'
                        sh 'terraform plan | tee terraform-plan.log'
                        sh 'terraform apply -auto-approve | tee terraform-apply.log'
                    }
                }
            }
        }
        stage('Deploy to EKS') {
            steps {
                script {
                    // Update kubeconfig for EKS
                    sh 'aws eks --region ${AWS_DEFAULT_REGION} update-kubeconfig --name eks'
                    
                    // Deploy to Kubernetes
                    sh "kubectl apply -f ./DEPI_Final_Project/Kubernetes/app-deployment.yaml"
                    sh "kubectl apply -f ./DEPI_Final_Project/Kubernetes/app-service.yaml"
                    
                    // Check deployed resources
                    sh 'kubectl get all'
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check the logs for details."
        }
    }
}
