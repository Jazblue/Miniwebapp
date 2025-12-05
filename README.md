# Miniwebapp

# Mini Web App on AWS

A highly available web application deployed on AWS using **CloudFormation**, **Application Load Balancer (ALB)**, **Auto Scaling Group (ASG)**, and **EC2 instances**. This project demonstrates a production-like web infrastructure with redundancy across two Availability Zones.

---

## Architecture

- **VPC & Networking**
  - Custom VPC with **two public subnets** in different Availability Zones.
  - Internet Gateway with proper route tables for internet access.

- **Security**
  - **ALB Security Group:** allows HTTP (80) from anywhere.
  - **EC2 Security Group:** allows HTTP only from the ALB SG.

- **Web Layer**
  - **Application Load Balancer (ALB):** internet-facing, distributes traffic to EC2 instances.
  - **Auto Scaling Group (ASG):** deploys EC2 instances across 2 AZs, ensures high availability.
  - **EC2 Instances:** Amazon Linux 2, Apache installed via **UserData**, serves a simple web page.

- **Health & Monitoring**
  - ALB target group health checks ensure EC2 instances are serving traffic.
  - Instances automatically replaced if unhealthy.

---

## Features

- Fully deployed via **CloudFormation** (infrastructure as code).  
- Load balancing across multiple AZs for high availability.  
- Auto Scaling Group ensures minimum and maximum instance capacity.  
- Web page served by EC2 instances via ALB.

---

## Deployment Instructions

Running the CloudFormation stack on Linux

Install and configure AWS CLI (if not already):

# Install AWS CLI v2 (example for Amazon Linux 2 / Ubuntu)
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

# Configure AWS CLI
aws configure


Enter AWS Access Key, Secret Key, default region (e.g., eu-west-2), and output format (json).

Clone the repository:

git clone https://github.com/Jazblue/Miniwebapp.git
cd Miniwebapp


Create the CloudFormation stack:

aws cloudformation create-stack \
    --stack-name mini-web \
    --template-body file://mini-web.yaml \
    --capabilities CAPABILITY_NAMED_IAM


Check stack status:

aws cloudformation describe-stacks \
    --stack-name mini-web \
    --query "Stacks[0].StackStatus"


Wait until it shows CREATE_COMPLETE.

Get the ALB DNS:

aws cloudformation describe-stacks \
    --stack-name mini-web \
    --query "Stacks[0].Outputs"


Access the web page:

# Use curl in Linux
curl http://<ALB_DNS_NAME>


You should see: Hello, Manchester United


Notes

No SSH KeyPair is required; EC2 instances are fully configured via UserData.

AMI is dynamically retrieved via SSM, ensuring it works in any AWS region.

The Auto Scaling Group currently has min=1 and max=3 instances. Scaling policies can be added for CPU-based auto-scaling.

Future Improvements

Add HTTPS support using AWS ACM.

Implement CloudWatch-based auto-scaling policies for real load-based scaling.

Deploy a dynamic web application or connect a backend database.

Author

Jase – Cloud enthusiast and Manchester United fan.


