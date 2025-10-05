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

architecture diagram:




**Quick Start Guide**
**1. Prerequisites**
AWS account with permissions to create VPCs, EC2, IGW, NAT Gateway, IAM roles, Security Groups.
AWS CLI installed and configured (aws configure).
Terraform or Ansible installed (depending on which IaC you use in this repo).
A local machine with SSH client. Keep your .pem private key secure and not committed to git.


Basic Prerequisites (detailed)

An AWS Account

IAM user with permissions: EC2FullAccess, VPCFullAccess, IAMFullAccess

AWS CLI installed and configured (aws configure)

Key pair for SSH access

Basic understanding of networking (CIDR, subnets, routing)
