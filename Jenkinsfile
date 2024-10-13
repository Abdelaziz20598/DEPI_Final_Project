// pipeline to build the terraform infrastucture on AWS..

pipeline {

    agent any    

    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository
                git branch: 'main',
                url: 'https://github.com/TOKA-FARID/ITI_Project'
            }
        }

        stage('initialize Terraform') {
            steps {
                dir('./terraform') {
                    script {
                        sh 'terraform init'
                    }
                }
            }
        }
        stage('Apply Terraform') {
            steps {
                dir('./terraform') {
                    script {
                        echo "Applying Terraform ...."
                        sh 'terraform apply -auto-approve'
                    }
                }
            }
        }

    }

        post {
            success {
                build job: 'AWS-Deploy-App', propagate: false
            }
        }

}