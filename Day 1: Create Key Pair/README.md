# Nautilus AWS Migration & Key Pair Setup

## Overview

This repository documents the process of migrating a portion of on-premises infrastructure to **AWS** and creating a secure **RSA key pair** (`nautilus-kp`) for SSH access. The migration is designed to be incremental to ensure minimal disruption, better control, and optimized resource management.

---

## Task Objectives

1. Create an **RSA key pair** in AWS:
   - **Key name:** `nautilus-kp`
   - **Key type:** `RSA`
2. Plan an **incremental migration** of servers to AWS.
3. Validate SSH access and connectivity using the newly created key.

---

## Key Pair Creation

### Using AWS CLI

```bash
# Create RSA key pair and save private key
aws ec2 create-key-pair \
    --key-name nautilus-kp \
    --key-type rsa \
    --query 'KeyMaterial' \
    --output text > nautilus-kp.pem

# Set correct permissions
chmod 400 nautilus-kp.pem