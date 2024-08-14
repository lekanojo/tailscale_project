# tailscale_project
Development of a tailscale subnet router and tailscale device

## Overview

This project demonstrates how to set up a secure private network using Tailscale, with two Amazon EC2 instances: one serving as a public-facing Tailscale subnet router and the other as a private Tailscale device. The public instance allows SSH access and routes traffic for the private instance through the Tailscale network, enabling secure communication between them.
A personal Tailnet was also created to manage resources from any devices; i.e web or mobile 

## Prerequisites

- **Terraform**: Used for managing infrastructure as code.
- **AWS CLI**: Configured with appropriate access permissions.
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
https://github.com/lekanojo/lekan_tailscale_infrastructure.git
cd lekan_tailscale_infrastructure


2. **Terraform Initialization**:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

3. **Accessing the EC2 Instances**:
   - Use SSH to connect to the public EC2 instance(subnet router)  and verify that Tailscale is set up correctly.
   - Use the public Ec2 instance (subnet router) to SSH into the private subnet (tailscale device)
  

## Architecture Diagram
(https://drive.google.com/file/d/1QAyhJDvTPpU5y9ej2RnRUiNORUA80jer/view?usp=sharing)

## Tailnet Information
- Tailnet Name: taile16727.ts.net

## Troubleshooting
If you encounter any issues:

- **Connectivity Issues:** Ensure the EC2 instances have the correct security group settings and that Tailscale is running properly.
- **Permission Errors:** Check that your AWS IAM role or user has the necessary permissions to create the resources.
- **Tailscale Issues:** Refer to the Tailscale documentation for troubleshooting tips.





