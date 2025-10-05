
---

### 🗂️ Folder: `/docs/`

#### 1. `implementation.md`

```markdown
# 🛠️ Step-by-Step Implementation Guide

## Step 1: Create VPC
- Go to **VPC → Create VPC**
- Name: `MyVPC`
- CIDR Block: `10.0.0.0/16`

## Step 2: Create Subnets
- Public Subnet: `10.0.1.0/24` (Enable Auto-assign Public IP)
- Private Subnet: `10.0.2.0/24`

## Step 3: Create Internet Gateway
- Attach IGW to your VPC

## Step 4: Create Route Tables
- Public RT → route `0.0.0.0/0` → IGW
- Private RT → route `0.0.0.0/0` → NAT Gateway

## Step 5: Configure NAT Gateway
- Create Elastic IP
- Launch NAT in the public subnet

## Step 6: Create Security Groups
- **Public SG:** Allow SSH (22), HTTP (80), HTTPS (443)
- **Private SG:** Allow inbound from Public SG only

## Step 7: Launch EC2 Instances
- One in public subnet, one in private
- Use your SSH key pair for access

## Step 8: IAM Role Configuration
- Create IAM Role with `AmazonEC2FullAccess`
- Attach to EC2 instance

## Step 9: Test Connectivity
- SSH into public EC2
- From there, SSH into private EC2 using private IP
- Verify internet access for private EC2 via NAT

---

## 🧩 Optional:
Automate setup using Terraform or Ansible later.
