# Continuous Integration/Continuous Deployment (CI/CD) Project Using Terraform, Kubernetes, Python, Jenkins, and AWS

Welcome to the repository housing a sophisticated CI/CD project designed to orchestrate a complete platform featuring a foundational "Hello, World!!" application. This project seamlessly integrates multiple technologies, including Terraform, Kubernetes (specifically Amazon EKS), Python, and Jenkins, to manage and deploy both infrastructure and application components.

## Project Overview

The primary objective of this project is to construct a comprehensive platform that encompasses a straightforward yet pivotal "Hello, World!!" application. This platform's infrastructure is containerized, and the application is deployed on Amazon EKS (Elastic Kubernetes Service), ensuring a scalable and efficient deployment.

## Pipelines

### 1. Infrastructure Pipeline
The infrastructure pipeline is dedicated to orchestrating the provisioning and management of the platform's AWS infrastructure using Terraform. It automates the setup and configuration of essential resources on the AWS cloud environment and triggers the subsequent CI/CD pipeline.

### 2. CI/CD Pipeline
The CI/CD pipeline is responsible for the continuous integration and deployment of the "Hello, World!!" application. This pipeline orchestrates the building, testing, containerization, and deployment of the application onto the EKS cluster. It is triggered by the successful execution of the Infrastructure Pipeline.

## Tools Employed
- **Terraform**: Utilized for defining and provisioning the infrastructure on AWS.
- **Kubernetes**: Specifically leveraging Amazon EKS for sophisticated container orchestration.
- **Python**: Integrated within the project, potentially used within the application or deployment scripts.
- **Jenkins**: Chosen to facilitate and automate the CI/CD pipelines.
- **AWS**: The primary cloud provider for hosting the infrastructure components.

## Workflow Overview
1. The infrastructure pipeline initializes and establishes the necessary infrastructure on AWS using Terraform, subsequently triggering the CI/CD pipeline.
2. The CI/CD pipeline automates the building, testing, containerization, and deployment of the "Hello, World!!" application onto the Amazon EKS cluster.

## Repository Structure
- `terraform/`: Contains comprehensive Terraform scripts for defining and provisioning the AWS infrastructure.
- `app/`: Houses the application code, potentially featuring a simple Python script that displays "Hello, World!!".
- `jenkins/`: Includes Jenkins pipeline configurations and scripts for managing both the infrastructure and application pipelines.

## Usage Instructions
To execute the infrastructure pipeline:
1. Navigate to the `terraform/` directory.
2. Utilize Terraform commands to initialize and apply the infrastructure scripts.

To execute the CI/CD pipeline:
1. Configure Jenkins and import the provided pipeline scripts from the `jenkins/` directory.
2. Trigger the CI/CD pipeline to build, test, containerize, and deploy the "Hello, World!!" application onto the EKS cluster.

## Additional Notes
- The pipelines are adaptable and can be tailored to accommodate different CI/CD tools, but for this project, Jenkins is the chosen tool.
- It is crucial to establish and manage appropriate AWS credentials and access for both the Terraform scripts and the EKS cluster.

Feel free to explore the provided directories and leverage the accompanying scripts to better understand and execute the CI/CD project efficiently.
