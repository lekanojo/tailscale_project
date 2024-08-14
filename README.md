# tailscale_project
Development of a tailscale subnet router and tailscale device

## Overview
This Terraform configuration is designed to set up a basic AWS infrastructure that consists of a Virtual Private Cloud (VPC) with both public and private subnets. The public subnet contains an EC2 instance acting as a Tailscale router, and the private subnet contains an EC2 instance acting as a Tailscale device. The configuration also includes Internet and NAT gateways, route tables, security groups, and outputs the public IP of the router and the private IP of the device.
A personal Tailnet was also created to manage resources from any devices; i.e web or mobile 

## Prerequisites

- **Terraform 0.12 or later**: Used for managing infrastructure as code.
- **AWS CLI**: Configured with appropriate access permissions.
- **SSH Key pair('ts-key')**: To be used for accessing EC2 instances
- **Tailscale Account**: Sign up at [Tailscale](https://tailscale.com/) if you don't have one.
- **Tailscale Authentication Key**: Generate a reusable auth key from your Tailscale account.

  
## Deployment code

- **provider.tf** - The primary Terraform configuration file that defines the infrastructure to be provisioned.  
- **network.tf** - Contains network information
- **variables.tf** - Contains variable definitions that are used across the Terraform configuration.
- **tailscale-subnet-router.tf** - Contains details about the public-facing ec2 instance representing the subnet router  
- **README.md** - This file, provides an overview, setup instructions, and other relevant information about the project.
- **architecture-diagram.png** - A visual representation of the infrastructure architecture.


## Setup Instructions

### 1. **Clone the Repository**

Begin by cloning this repository to your local machine:

```bash
git clone https://github.com/yourusername/tailscale_project.git
cd tailscale_project
```

2. **Terraform Variables**:
[Terraform Variables: Create a terraform.tfvars file in the root directory to define the following variables:
```bash
aws_region = "us-east-1"  
aws_profile = "your-aws-profile"  
ssh_private_key = "path-to-your-private-key"
```

```bash
aws_region      = "us-east-1"
aws_profile     = "your-aws-profile"
ssh_private_key = "~/.ssh/ts-key.pem"
```


3. **Terraform Initialization**:

   -**terraform init**: Initialize your Terraform working directory, which will download the necessary provider plugins
   -**terraform plan**: You can preview the changes Terraform will make before applying them
   -**terraform apply**: Apply the configuration to create the infrastructure. Type yes when prompted to confirm the changes.
     

3. **Accessing the EC2 Instances**:
   After the infrastructure is created, you can SSH into the EC2 instances:

  Tailscale Router (Public EC2 Instance):
```bash
 ssh -i /path/to/ts-key.pem ubuntu@<tailscale_router_public_ip>
```

Tailscale Device (Private EC2 Instance):
First, SSH into the Tailscale Router, then connect to the private instance from there.

## Clean Up
To destroy the infrastructure when you are done; use 
terraform destroy
Type 'Yes' when prompted to confirm the destruction

## Components

1. **AWS Provider Configuration**: Defines the AWS provider and configures it using variables for the region and profile.
```bash
   provider "aws" {
  region  = var.aws_region
  profile = var.aws_profile
}
```
2. **VPC**: Creates a VPC with DNS support and hostnames enabled.
```bash
resource "aws_vpc" "main_vpc" {
  cidr_block = "10.0.0.0/16"
  enable_dns_support = true
  enable_dns_hostnames = true

  tags = {
    Name = "main-vpc"
  }
}
```



3. Subnets
Public Subnet:

hcl
Copy code
resource "aws_subnet" "public_subnet" {
  vpc_id            = aws_vpc.main_vpc.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"
  tags = {
    Name = "public-subnet"
  }
}
Private Subnet:

hcl
Copy code
resource "aws_subnet" "private_subnet" {
  vpc_id            = aws_vpc.main_vpc.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1a"
  tags = {
    Name = "private-subnet"
  }
}










   
## Architecture Diagram
(https://drive.google.com/file/d/1QAyhJDvTPpU5y9ej2RnRUiNORUA80jer/view?usp=sharing)

## Tailnet Information
- Tailnet Name: taile16727.ts.net

## Troubleshooting
If you encounter any issues:

- **Connectivity Issues:** Ensure the EC2 instances have the correct security group settings and that Tailscale is running properly.
- **Permission Errors:** Check that your AWS IAM role or user has the necessary permissions to create the resources.
- **Tailscale Issues:** Refer to the Tailscale documentation for troubleshooting tips.





