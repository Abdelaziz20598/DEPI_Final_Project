CI/CD Project with Terraform, Kubernetes, Python, Jenkins, and AWS

Welcome to this CI/CD project repository, designed to automate infrastructure provisioning and application deployment using Terraform, Kubernetes (Amazon EKS), Python, Jenkins, and AWS.

Overview

This project establishes a scalable platform featuring a containerized "Hello, World!" application. The infrastructure is provisioned using Terraform, and the application is deployed on Amazon EKS via an automated CI/CD pipeline.

Pipelines

1. Infrastructure Pipeline

Automates the provisioning and management of AWS infrastructure using Terraform. Upon successful execution, it triggers the CI/CD pipeline.

2. CI/CD Pipeline

Handles the continuous integration and deployment of the "Hello, World!" application. This includes building, testing, containerizing, and deploying the application to the EKS cluster.

Technologies Used

Terraform – Infrastructure as Code (IaC) for AWS resource provisioning.

Kubernetes (EKS) – Container orchestration for scalable application deployment.

Python – Used within the application or deployment scripts.

Jenkins – Automates CI/CD processes.

AWS – Cloud provider hosting the infrastructure components.

Workflow

Infrastructure Pipeline: Deploys AWS infrastructure using Terraform and triggers the CI/CD pipeline.

CI/CD Pipeline: Builds, tests, containerizes, and deploys the application onto Amazon EKS.

Repository Structure

terraform/ – Terraform scripts for AWS infrastructure provisioning.

app/ – Application source code (Python-based "Hello, World!").

jenkins/ – Jenkins pipeline configurations and automation scripts.

Usage

Running the Infrastructure Pipeline

Navigate to the terraform/ directory.

Execute Terraform commands to initialize and apply infrastructure scripts:

terraform init
terraform apply

Running the CI/CD Pipeline

Configure Jenkins and import pipeline scripts from jenkins/.

Trigger the pipeline to build, test, containerize, and deploy the application to EKS.

Additional Notes

Pipelines can be customized for other CI/CD tools if needed.

Proper AWS credentials and access permissions are required for Terraform and EKS.

Explore the repository and leverage the provided scripts to efficiently deploy and manage the CI/CD project.


