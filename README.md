<img width="1024" height="1536" alt="a929627f-5577-4d6d-bc59-3b1ef53a0fad" src="https://github.com/user-attachments/assets/89311390-c2da-4844-a84e-8ff43dd0541b" /># AWS SOC Analyst Lab

## Objective
Simulate a Security Operations Center (SOC) in AWS using CloudTrail, GuardDuty, Security Hub, and a SIEM to monitor, detect, and respond to threats.



## Project Phases
1. AWS Account Setup & Security Baseline
2. CloudTrail & CloudWatch Logging
3. GuardDuty Configuration & Findings
4. SIEM Setup & Dashboard
5. Incident Response & Playbooks
6. ## Deliverables
- Architecture diagrams
- SIEM dashboards
- Sample alerts & responses
- Documentation of each phase



# AWS SOC Analyst Lab – Phase 1: Architecture Setup ✅

This document outlines the completed setup for **Phase 1** of the AWS SOC Analyst Lab. This phase focuses on building the foundational cloud infrastructure to simulate a secure enterprise environment.

---

## 🧱 VPC Configuration

- **VPC Name**: `SOC-VPC`
- **CIDR Block**: `10.0.0.0/16`
- **Tenancy**: Default

---

## 🌐 Subnets

| Subnet Name         | Type    | CIDR Block   | Availability Zone |
|---------------------|---------|--------------|-------------------|
| SOC-Public-Subnet   | Public  | 10.0.1.0/24  | e.g., us-east-1a  |
| SOC-Private-Subnet  | Private | 10.0.2.0/24  | e.g., us-east-1a  |

---

## 🚪 Internet Gateway

- **Name**: `SOC-IGW`
- **Attached to**: `SOC-VPC`

---

## 🛣️ Route Tables

### Public Route Table
- **Name**: `SOC-Public-RT`
- **Associated Subnet**: `SOC-Public-Subnet`
- **Routes**:
  - `0.0.0.0/0` → `SOC-IGW`

---

## 🔐 Security Groups

### SOC-Web-SG (Linux Web Server)
| Type   | Protocol | Port | Source           | Description         |
|--------|----------|------|------------------|---------------------|
| SSH    | TCP      | 22   | Your IP          | Remote access       |
| HTTP   | TCP      | 80   | 0.0.0.0/0        | Web traffic         |
| HTTPS  | TCP      | 443  | 0.0.0.0/0        | Secure web traffic  |

### SOC-AD-SG (Windows AD Server)
| Type   | Protocol | Port | Source           | Description               |
|--------|----------|------|------------------|---------------------------|
| RDP    | TCP      | 3389 | Your IP          | Remote desktop access     |
| LDAP   | TCP      | 389  | 10.0.2.0/24      | AD communication          |
| DNS    | UDP      | 53   | 10.0.2.0/24      | Internal DNS resolution   |
| SMB    | TCP      | 445  | 10.0.2.0/24      | File sharing              |

---

## ✅ Status

- [x] VPC created
- [x] Subnets configured
- [x] Internet Gateway attached
- [x] Route Table configured
- [x] Security Groups created

---

# 🛡️ SOC Analyst Lab – Phase 2: EC2 Web Server Deployment

## ✅ Objective
Successfully deploy and publicly access an Apache HTTPD web server on an EC2 instance as part of the SOC Analyst Lab.

---

## 🖥️ EC2 Instance Configuration

- **AMI**: Amazon Linux 2
- **Instance Type**: t2.micro
- **Subnet**: SOC-Public-Subnet
- **Security Group**: SOC-Web-SG
- **Ports Opened**:
  - SSH (22) – for remote access
  - HTTP (80) – for public web access
- **Public IP Assigned**: Yes

---

## 🔧 Apache HTTPD Setup

Commands executed on the EC2 instance:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd


📌 Next Steps

Proceed to:

Install CloudWatch Agent for log monitoring
Enable AWS CloudTrail, GuardDuty, and Security Hub
Configure centralized logging to Amazon S3
