// pipeline to build the terraform infrastucture on both AWS and EKS..

pipeline {
    agent any

    environment {//needs to be changed
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
        //ECR_REPOSITORY = "1410-8352-5350.dkr.ecr.us-east-1.amazonaws.com/flask-app"
        DOCKER_REPO = "abdelaziz20598/depi-flask:last"
        GIT_REPO_URL = "https://github.com/Abdelaziz20598/DEPI_Final_Project.git"
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                git branch: 'master', url: "${GIT_REPO_URL}"
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

        stage('Build Docker Image') {
            steps {
                dir('./DEPI_Final_Project/App') {
                    script {
                        sh 'docker build -t my-app .'
                        //sh "docker tag my-app ${ECR_REPOSITORY}:latest"
                        sh "docker tag my-app ${DOCKER_REPO}:latest"
                        sh "docker push ${DOCKER_REPO}:latest"
                        
                    }
                }
            }
        }
/*
        stage('Configure Docker Registry') {
            steps {
                script {
                    sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${ECR_REPOSITORY}"
                }
            }
        }
*/
        /*
        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${ECR_REPOSITORY}:latest"
                }
            }
        }
*/
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
