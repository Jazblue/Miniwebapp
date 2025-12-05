Mini Web App – CloudFormation Demo

This project demonstrates a full AWS infrastructure deployment using CloudFormation, including VPC, ALB, Auto Scaling, and EC2 instances. The demo also features a Manchester United-themed web page running on multiple EC2 instances across 2 Availability Zones.

Features

Fully automated infrastructure with CloudFormation

VPC + 2 Public Subnets for multi-AZ deployment

Application Load Balancer (ALB) with a Target Group

Auto Scaling Group (ASG) with 2–3 EC2 instances

UserData scripts printing hostname and Availability Zone

Manchester United themed demo showing dynamic content per instance

Verified Load Balancing: ALB distributes traffic across instances

Verified Auto Scaling: ASG launches new instances under load (tested with Apache Bench)

ASG Load Test (Optional Demo Section)

Load tested ALB using Apache Bench (ab) with 500 requests and concurrency of 10.

ASG detected load and launched additional EC2 instances automatically.

Refreshing the ALB URL shows hostnames changing across multiple instances, confirming traffic distribution.
## Screenshots

### 1️⃣ CloudFormation Stack Created
![CloudFormation Stack Created](cloudformation1.PNG)

### 2️⃣ CloudFormation Resources
![CloudFormation Resources](cloudformation2.PNG)

### 3️⃣ ALB Example – First Instance
![ALB Screenshot 1](alb1.PNG)

### 4️⃣ ALB Example – Second Instance
![ALB Screenshot 2](alb2.PNG)

> Refreshing the ALB URL shows traffic being distributed across multiple EC2 instances.

## How to Deploy

1. Ensure you have an **AWS Key Pair** (e.g., `miniweb-key`) and AWS CLI configured.
2. Clone this repo:

```bash
git clone https://github.com/Jazblue/Miniwebapp.git
cd Miniwebapp
