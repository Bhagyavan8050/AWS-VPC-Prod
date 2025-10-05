# Deep Dive Explanation of AWS VPC Project

## 1. Project Overview

This project demonstrates how to design and deploy a **custom AWS Virtual Private Cloud (VPC)** with both public and private subnets, EC2 instances, secure access control, and routing configurations. It replicates a **real-world enterprise-level networking setup** where:

* Public resources (like web servers) can be accessed via the Internet.
* Private resources (like databases) remain secure and isolated.

---

## 2. Core Objectives

| Goal                              | Description                                                                      |
| --------------------------------- | -------------------------------------------------------------------------------- |
| **Network Design**                | Create a logically isolated network using AWS VPC with CIDR-based IP allocation. |
| **Public and Private Subnets**    | Separate workloads based on exposure and functionality.                          |
| **Routing and NAT Configuration** | Allow secure internet connectivity for public and private subnets.               |
| **Security Hardening**            | Control access using Security Groups, NACLs, and IAM roles.                      |
| **Connectivity Testing**          | Verify SSH access and network reachability across subnets.                       |

---

## 3. VPC and Networking Design

### Components Created:

1. **VPC**

   * Custom VPC CIDR: `10.0.0.0/16`
   * Provides the private IP range for all resources.

2. **Subnets**

   * **Public Subnet (10.0.1.0/24)** → For EC2 instances needing internet access.
   * **Private Subnet (10.0.2.0/24)** → For backend servers, databases, etc.

3. **Internet Gateway (IGW)**

   * Attached to the VPC to enable **outbound/inbound** internet access for public subnets.

4. **NAT Gateway**

   * Deployed in the public subnet to allow **private subnet** instances to access the Internet (for updates, patches, etc.) **without exposing them directly**.

5. **Route Tables**

   * **Public Route Table** → Routes all `0.0.0.0/0` traffic via **Internet Gateway**.
   * **Private Route Table** → Routes all `0.0.0.0/0` traffic via **NAT Gateway**.

---

## 4. Security Layers

### Security Groups

* Virtual firewalls attached to EC2 instances.
* Example rules:

  * Allow **SSH (22)** from your IP to bastion host.
  * Allow **HTTP (80)** or **HTTPS (443)** from anywhere to web servers.
  * Allow **Private-to-Private communication** between internal instances.

### Network ACLs (NACLs)

* Stateless filters applied at subnet level.
* Used to **add another layer of protection** beyond security groups.

### IAM Roles & Policies

* Roles are attached to EC2 instances to allow specific AWS actions.
* Example: S3 Read-only role for private EC2 instance.

---

## 5. Instance Deployment

* **Public EC2 Instance (Bastion Host):**

  * Acts as a **jump server** for SSH access to private instances.
  * Accessible from the Internet using SSH key pair.

* **Private EC2 Instance:**

  * Deployed in private subnet.
  * No direct Internet access.
  * Can connect to Internet through NAT Gateway.
  * Accessed **via Bastion Host** (using SSH agent forwarding or jump host).

---

## 6. Access Management

1. Generate a new **SSH key pair** (`.pem` file).
2. Set proper permissions (`chmod 400 key.pem`).
3. Access flow:

   ```
   Your Laptop → Bastion Host (Public Subnet) → Private Instance (Private Subnet)
   ```
4. IAM roles ensure least privilege and prevent over-permissioning.

---

## 7. Testing and Validation

| Test                        | Description                               | Expected Result    |
| --------------------------- | ----------------------------------------- | ------------------ |
| **SSH Access**              | Connect to public instance using PEM key. | Successful         |
| **Private Instance Access** | SSH into private instance via Bastion.    | Successful         |
| **Internet Access**         | Ping external IP from private instance.   | Successful via NAT |
| **Internal Connectivity**   | Ping between instances in same VPC.       | Successful         |
| **Security Rules**          | Block unauthorized ports or IPs.          | Denied             |

---

## 8. Security Considerations

 Use least privilege IAM roles  
 Restrict inbound SSH by specific IP  
 Regularly rotate keys and credentials  
 Enable flow logs for VPC for monitoring  
 Avoid using default VPC for production setups

---

## 9. Troubleshooting

| Issue                                  | Possible Cause                    | Solution                          |
| -------------------------------------- | --------------------------------- | --------------------------------- |
| SSH timeout                            | SG or NACL blocking port 22       | Update inbound rule for SSH       |
| Internet not working in private subnet | NAT not attached or route missing | Check route table and NAT gateway |
| Can’t reach private EC2                | Bastion host misconfigured        | Verify jump host setup and key    |

---


