**Project Overview**
This repository contains IaC and deployment instructions for building a secure, production-like AWS VPC environment. The goal is to demonstrate best-practice network design, secure access patterns (bastion host), outbound internet via NAT, and least-privilege IAM usage for EC2 instances.

**Key outcomes:**
Custom VPC with public and private subnets
Internet Gateway (IGW) for public networking
NAT Gateway for private subnet outbound access
Route tables and subnet associationsSecurity Groups and NACLs for layered security
EC2 instances in both public/private
subnets (bastion + app)
IAM roles for EC2 (no hard-coded credentials)
Validation tests and troubleshooting guides.

**Architecture diagram:**
![image alt](https://github.com/Bhagyavan8050/AWS-VPC-Prod/blob/55b9085bf37cc4c337c7a1d30618bd1022254c25/Architecture.png)


**Quick Start Guide**
**1. Prerequisites**
AWS account with permissions to create VPCs, EC2, IGW, NAT Gateway, IAM roles, Security Groups.
AWS CLI installed and configured (aws configure).
Terraform or Ansible installed (depending on which IaC you use in this repo).
A local machine with SSH client. Keep your .pem private key secure and not committed to git.


**Basic Prerequisites (detailed)**
An AWS Account
IAM user with permissions: EC2FullAccess, VPCFullAccess, IAMFullAccess
AWS CLI installed and configured (aws configure)
Key pair for SSH access
Basic understanding of networking (CIDR, subnets, routing)


**Documentation**
Detailed setup steps are located in the /docs/ folder:
/docs/implementation.md – Full step-by-step VPC setup
/docs/troubleshooting.md – Common issues and fixes
/docs/security.md – Security best practices
/docs/screenshots.md – Architecture & AWS console screenshots.

**Screenshots**
| Component         | Description                                  |
| ----------------- | -------------------------------------------- |
| VPC Overview      | Shows created VPC, subnets, and route tables |
| EC2 Instances     | Instances in public and private subnets      |
| Security Groups   | Inbound/Outbound rules                       |
| Connectivity Test | Successful SSH & ping results                |


**Useful Links**
[AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
[AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
[AWS IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
[CIDR Calculator](https://www.ipaddressguide.com/cidr)


**👨‍💻 Author**
Bhagyavan Bhange
DevOps Engineer | AWS | Terraform | Jenkins | Ansible
Email: Bhagyavanbhange8050@gmail.com
LinkedIn: [ProfileLink](https://www.linkedin.com/in/bhagyavan-bhange-1196a0227/)

