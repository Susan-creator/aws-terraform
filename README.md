# Jenkins on Docker using AWS EC2 and Terraform

This project provisions an AWS EC2 instance running Jenkins inside a Docker container using Terraform. The infrastructure is managed as code to ensure easy reproducibility and scalability.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [Usage](#usage)
- [Outputs](#outputs)

## Overview

The Terraform configuration will:
- Create an AWS EC2 instance with Ubuntu 22.04.
- Install Docker and run Jenkins in a Docker container.
- Set up security group rules to allow access to Jenkins from your IP.

## Prerequisites

To get started, ensure you have the following installed and configured:
- An [AWS account](https://aws.amazon.com/)
- [AWS CLI](https://aws.amazon.com/cli/)
- [Terraform](https://www.terraform.io/downloads.html)
- AWS IAM credentials with permissions to create EC2 instances and security groups

## Configuration

Terraform files used in this project:
1. `main.tf`: Specifies the AWS provider and region.
2. `jenkins-ec2.tf`: Provisions an EC2 instance and installs Docker and Jenkins.
3. `networking.tf`: Creates a security group to allow traffic from your IP.
4. `outputs.tf`: Displays the EC2 instance's public IP.
5. `variables.tf`: Contains variables for your IP and key pair name.
6. `terraform.tfvars`: Stores the sensitive values for variables.

## Usage

1. Clone the repository and navigate to the directory:

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Initialize Terraform:

    ```bash
    terraform init
    ```

3. Preview the changes:

    ```bash
    terraform plan
    ```

4. Apply the configuration:

    ```bash
    terraform apply
    ```

5. Once the Terraform run is complete, Jenkins will be running on the EC2 instance.

## Outputs

After running `terraform apply`, you will see the EC2 instance's public IP. To access Jenkins:
- Open your browser and enter the instance's public IP followed by port `8080`:

    ```
    http://<public-ip>:8080
    ```

- The Jenkins unlock password is in the Docker container logs. Use the following command to retrieve it:

    ```bash
    sudo docker logs jenkins
    ```

## Cleanup

To destroy the created resources, run:

```bash
terraform destroy
