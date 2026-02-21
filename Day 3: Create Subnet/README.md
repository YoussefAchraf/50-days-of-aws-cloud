# Day 4: Create DevOps Subnet

## Overview

In this task, I set up a new **subnet** named `devops-subnet` within the **default VPC** of our AWS environment. This subnet will serve as a dedicated network segment for DevOps resources and tools, supporting the incremental migration strategy for our infrastructure.

This README explains the steps I followed, the commands I executed, and how I verified the subnet creation.

---

## Task Objectives

The main objectives of this task were:

1. **Identify the default VPC** in the AWS region to ensure the subnet is created in the correct network.
2. **Create a new subnet** named `devops-subnet` within the default VPC, selecting an available CIDR block that does not conflict with existing subnets.
3. **Verify subnet creation** and confirm its availability for use with AWS resources.

---

## Subnet Creation

I created the subnet using the **AWS CLI**, which allowed for precise CIDR allocation and automated tagging.

### Commands Used

```bash
# Step 1: Get the Default VPC ID
aws ec2 describe-vpcs \
    --filters "Name=isDefault,Values=true" \
    --query "Vpcs[0].VpcId" \
    --output text

# Step 2: Check the CIDR block of the Default VPC
aws ec2 describe-vpcs \
    --vpc-ids <DEFAULT_VPC_ID> \
    --query "Vpcs[0].CidrBlock" \
    --output text

# Step 3: List existing subnets to avoid CIDR conflicts
aws ec2 describe-subnets \
    --filters "Name=vpc-id,Values=<DEFAULT_VPC_ID>" \
    --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock,AZ:AvailabilityZone,Name:Tags[?Key=='Name']|[0].Value}" \
    --output table

# Step 4: Create a new subnet in an available CIDR range
aws ec2 create-subnet \
    --vpc-id <DEFAULT_VPC_ID> \
    --cidr-block <AVAILABLE_CIDR_BLOCK> \
    --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=devops-subnet}]'

# Step 5: Verify the new subnet is available
aws ec2 describe-subnets \
    --filters "Name=vpc-id,Values=<DEFAULT_VPC_ID>" \
    --query "Subnets[*].{ID:SubnetId,Name:Tags[?Key=='Name']|[0].Value,CIDR:CidrBlock}" \
    --output table