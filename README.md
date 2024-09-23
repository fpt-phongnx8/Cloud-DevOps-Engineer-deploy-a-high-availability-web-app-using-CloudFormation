# Udagram Infrastructure as Code Project

---

## Project Overview
This project sets up the complete infrastructure for the Udagram application using AWS CloudFormation. It consists of network configuration and server deployment that support a highly available, scalable web application named Udagram.

![Udagram Architecture](/diagram/Infrastructure-Diagram.png)

## Architecture
The infrastructure is defined across several CloudFormation scripts:
- **Network Stack**: Network resources: VPC, subnets, Internet Gateway, NAT Gateways
- **Server Stack**: EC2 resources: Autoscaling group with EC2 instances, Load Balancer, Security Groups
- **Static Content**: S3 bucket.

## Directory Structure

- `templates/`: Contains all the CloudFormation YAML templates.
- `parameters/`: JSON files for template parameters.
- `*.sh/`: Shell scripts to automate the deployment.
- `diagram/`: Diagram.

## Prerequisites
To run this project, you will need:
- AWS CLI installed and configured with an IAM user that has the necessary permissions.
- An S3 bucket to store the CloudFormation templates (optional, improves performance for large templates).
- Key pairs for SSH access to EC2 instances (see `create_keypair.sh`).

## Setup Instructions

### 1. Clone the Repository
Clone this repository to your local machine:
```bash
git clone https://github.com/fpt-phongnx8/Cloud-DevOps-Engineer-deploy-a-high-availability-web-app-using-CloudFormation udagram-project 
cd udagram-project
```

### 2. Create the Network Infrastructure
Run the network setup script:
```bash
chmod +x *.sh
./create_network.sh
```

### 3. Deploy the Servers
After the network stack is complete, deploy the servers:
```bash
./create_udagram.sh
```

### 4. Verify Deployment
Check the AWS CloudFormation console to ensure that stacks are created without errors. You should see outputs such as URLs or instance IDs in the console.

## Cleanup
To delete the stacks and avoid ongoing charges:
```bash
aws cloudformation delete-stack --stack-name udagram-iac-network --region us-east-1
aws cloudformation delete-stack --stack-name udagram-iac-server --region us-east-1
```

URL: http://udagra-webap-mwvmnnszuhnh-559332658.us-east-1.elb.amazonaws.com/

