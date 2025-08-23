# AWS VPC Three-Tier Architecture


## Overview
# 🏗️ AWS VPC Three-Tier Architecture

This project demonstrates a production-grade deployment of a **three-tier VPC architecture** using AWS CloudFormation. It includes:

- ✅ Public subnet with Auto Scaling Group and S3 Bucket
- 🔐 Private subnets for Application and Database tiers.
- 🌐 Internet Gateway and secured internet access
- 🛡️ Security Groups and Route Tables for tier isolation
- 📦 Modular CloudFormation templates for easy deployment

---

## 📐 Architecture Overview

![Architecture Diagram](assets/architecture-diagram.png)

### 🔹 Tier Breakdown

| Tier | Subnet Type | Components |
|------|-------------|------------|
| **Public Tier** | Public Subnet | EC2 Instances, Auto Scaling Group, S3 Bucket |
| **App Tier**    | Private Subnet |  API Gateway, Lambda Functions|
| **DB Tier**     | Private Subnet | RDS or EC2-based database |

---

## 📁 GitHub Repo Structure: aws-vpc-three-tier-architecture
```
├── LICENSE - MIT-0 License file
├── README.md - This file
├── assets - Images and diagrams
├── templates - CloudFormation templates
│   ├── app-tier.yaml - Application tier CloudFormation template
│   ├── db-tier.yaml - Database tier CloudFormation template
│   └── vpc.yaml - VPC CloudFormation template
└── scripts - Scripts for deployment
    ├── deploy-app-tier.sh - Deploy Application tier CloudFormation stack
    ├── deploy-db-tier.sh - Deploy Database tier CloudFormation stack
    └── deploy-vpc.sh - Deploy VPC CloudFormation stack
    └── destroy-all.sh - Destroy all CloudFormation stacks
```

---

## 🧱 Infrastructure Components

- **VPC** with CIDR block `10.0.0.0/16`
- **2 Availability Zones** for high availability
- **Public Subnet** with IGW and Auto Scaling Group
- **Private Subnets** with API Gateway, Lambda Functions, and RDS or EC2-based database
- **Security Groups** for tier isolation and controlled access
- **Route Tables** for subnet-level routing
- **CloudFormation Templates** for modular deployment

---

## 🚀 Deployment Instructions

### 1️⃣ Deploy the VPC and Networking Stack

```bash
aws cloudformation deploy \
  --template-file templates/vpc.yaml \
  --stack-name vpc-stack \
  --capabilities CAPABILITY_NAMED_IAM
  --parameter-overrides VpcCidr=10.0.0.0/16 AvailabilityZones=us-east-1a,us-east-1b
```

### 2️⃣ Deploy the Application Tier Stack

```bash
aws cloudformation deploy \
  --template-file templates/app-tier.yaml \
  --stack-name app-tier-stack \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides VpcId=<VPC_ID> VpcCidr=10.0.0.0/16 AvailabilityZones=us-east-1a,us-east-1b
```

### 3️⃣ Deploy the Database Tier Stack

```bash
aws cloudformation deploy \
  --template-file templates/db-tier.yaml \
  --stack-name db-tier-stack \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides VpcId=<VPC_ID> VpcCidr=10.0.0.0/16 AvailabilityZones=us-east-1a,us-east-1b
```

---

## 🔐 Security Highlights
- VPC Flow Logs enabled for all traffic
- Security Groups and Route Tables configured for tier isolation
- Bastion Host with SSH access to private subnets
- NAT Gateway for outbound internet access
- EC2 Instances and Auto Scaling Groups in private subnets
- DB tier locked down to App tier only
- NAT Gateway used for secure outbound traffic from private subnets

---

## 👤 Author

 **DCyberguy**
website: https://playroom-security.com

## 📝 License

This library is licensed under the MIT-0 License. See the LICENSE file.
