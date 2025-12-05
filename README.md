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

1. Clone this repository:

```bash
git clone <repository-url>
cd <repository-folder>

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


