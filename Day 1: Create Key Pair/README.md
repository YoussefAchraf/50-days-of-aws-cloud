# Nautilus AWS Migration & Key Pair Setup

## Overview

In this project, I handled the migration of part of the Nautilus on-premises infrastructure to **AWS**, focusing on **secure access** via an RSA key pair. The goal was to ensure safe SSH connectivity to EC2 instances while planning the migration incrementally to minimize disruption, maintain control, and optimize resource usage.

This README explains the steps I followed, the commands I executed, and how I validated the migration and key pair setup.

---

## Task Objectives

The main objectives of this task were:

1. **Create an RSA key pair in AWS** for secure SSH access:
   - **Key name:** `nautilus-kp`
   - **Key type:** `RSA`
2. **Plan an incremental migration** of on-premises servers to AWS, grouping servers by purpose.
3. **Validate SSH access and connectivity** using the newly created key to ensure secure and reliable access.

---

## Key Pair Creation

I generated the RSA key pair using the **AWS CLI** to automate and securely download the private key.

### Command Used

```bash
# Create an RSA key pair named nautilus-kp and save the private key locally
aws ec2 create-key-pair \
    --key-name nautilus-kp \
    --key-type rsa \
    --query 'KeyMaterial' \
    --output text > nautilus-kp.pem