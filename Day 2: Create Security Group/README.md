# Nautilus AWS Migration – Day 2: Create Security Group

## Overview

In this project, I created a **Security Group** in the **default VPC** for Nautilus application servers. The goal was to allow **HTTP (port 80)** traffic for web access and **SSH (port 22)** for secure remote administration, while preparing the infrastructure for incremental migration to AWS.

This README explains the commands I executed to create the security group and configure its inbound rules.

---

## Task Objectives

The main objectives of this task were:

1. **Create a Security Group** in the default VPC:
   - **Name:** `devops-sg`
   - **Description:** `Security group for Nautilus App Servers`
2. **Add inbound rules** to allow required traffic:
   - HTTP: Port 80, Source `0.0.0.0/0`
   - SSH: Port 22, Source `0.0.0.0/0`
3. **Validate the security group** to ensure correct configuration.

---

## Security Group Creation

I created the security group and configured the required inbound rules using the **AWS CLI**.

### Commands Used

```bash
# Get the default VPC ID
aws ec2 describe-vpcs \
    --filters "Name=isDefault,Values=true" \
    --query "Vpcs[0].VpcId" \
    --output text

# Create the security group
aws ec2 create-security-group \
    --group-name devops-sg \
    --description "Security group for Nautilus App Servers" \
    --vpc-id <VPC-ID>

# Add HTTP inbound rule
aws ec2 authorize-security-group-ingress \
    --group-id <SG-ID> \
    --protocol tcp \
    --port 80 \
    --cidr 0.0.0.0/0

# Add SSH inbound rule
aws ec2 authorize-security-group-ingress \
    --group-id <SG-ID> \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0

# Verify the security group
aws ec2 describe-security-groups \
    --group-ids <SG-ID>