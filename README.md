# Terraform Setup in AWS CloudShell

This repository provides a quick guide to installing and running [Terraform](https://www.terraform.io/) inside **AWS CloudShell** — a browser-based shell provided by AWS for managing cloud resources.

## Why Use Terraform in AWS CloudShell?

AWS CloudShell provides:
- Secure and pre-authenticated access to your AWS environment.
- Persistent $HOME directory for storing configuration files and binaries.
- No local setup required — use Terraform from any browser.

However, Terraform does **not come pre-installed** in AWS CloudShell. 

This guide enables you to set it up manually.

---

## Installation Script

1. Run the following script in **AWS CloudShell** to install Terraform:

```bash
# Set the Terraform version you want to install
TERRAFORM_VERSION="1.8.2"

# Install unzip and wget (if not already available)
sudo yum install -y unzip wget

# Download Terraform
wget https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip

# Unzip the Terraform binary
unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip

# Move the binary to /usr/local/bin so it's globally accessible
sudo mv terraform /usr/local/bin/

# Clean up the zip file
rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip

# Verify installation
terraform version

```
---
Verifying the Installation

After the script runs successfully, you should see an output like:

```
Terraform v1.8.2
on linux_amd64

```
This confirms Terraform is installed and ready to use.

Next Steps

You can now:

Create and manage AWS infrastructure as code using .tf files.

Use Terraform commands such as init, plan, apply, and destroy directly from CloudShell.

Troubleshooting
---
Permission Denied: If you get permission issues with /usr/local/bin, try using a local $HOME/bin directory and updating your PATH:

```
mkdir -p ~/bin
mv terraform ~/bin/
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

Terraform Not Found: Run which terraform to ensure it’s correctly added to your PATH.

```

2. Test the install/simple-s3-bucket/main.tf

> A minimal example to validate that Terraform works and can create a resource.

```

provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name
  acl    = "private"
}
```
variables.tf
```
variable "region" {
  description = "AWS region"
  default     = "us-east-1"
}

variable "bucket_name" {
  description = "Name of the S3 bucket"
}
```
outputs.tf
```
output "bucket_name" {
  value = aws_s3_bucket.example.id
}
```
Feedback & Contributions

Feel free to submit issues or pull requests if you’d like to improve this setup or add enhancements.
```
