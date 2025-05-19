# terraform-aws-cloudshell-setup

Repository Structure

terraform-aws-cloudshell-setup/

    ├── README.md

    ├── install-terraform.sh

    ├── examples/

    │   └── simple-s3-bucket/

    │       ├── main.tf

    │       ├── variables.tf

    │       └── outputs.tf

    ├── LICENSE


install-terraform.sh

> The install script referenced in your README.

#!/bin/bash

# install-terraform.sh
# Script to install Terraform in AWS CloudShell

set -e

TERRAFORM_VERSION="1.8.2"

echo "Installing dependencies..."
sudo yum install -y unzip wget

echo "Downloading Terraform v$TERRAFORM_VERSION..."
wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip

echo "Unzipping Terraform..."
unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip

echo "Moving Terraform binary to /usr/local/bin/..."
sudo mv terraform /usr/local/bin/

echo "Cleaning up..."
rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip

echo "Verifying installation..."
terraform version

Make it executable with:

chmod +x install-terraform.sh


2. test the install/simple-s3-bucket/main.tf

> A minimal example to validate that Terraform works and can create a resource.

provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
  acl    = "private"
}

variables.tf

variable "region" {
  description = "AWS region"
  default     = "us-east-1"
}

variable "bucket_name" {
  description = "Name of the S3 bucket"
}

outputs.tf

output "bucket_name" {
  value = aws_s3_bucket.example.id
}


