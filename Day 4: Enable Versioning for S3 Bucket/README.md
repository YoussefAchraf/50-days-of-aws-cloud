# Nautilus S3 Bucket Versioning Setup

## Overview

In this project, I implemented **versioning** for the S3 bucket `nautilus-s3-3215`. Enabling versioning ensures that all object versions are retained, allowing recovery in case of accidental deletion or corruption. This task is part of data protection and recovery measures for the Nautilus AWS infrastructure.

This README explains the objectives, commands used, and verification steps for enabling versioning on the S3 bucket.

---

## Task Objectives

The main objectives of this task were:

1. **Enable versioning** on the S3 bucket:
   - **Bucket name:** `nautilus-s3-3215`
   - **Versioning status:** Enabled
2. **Ensure recoverability** of objects in case of accidental deletion or modification.
3. **Validate versioning** to confirm that multiple object versions can be maintained.

---

## Enabling Versioning

I enabled versioning using the **AWS CLI** for automation and consistency.

### Command Used

```bash
# Enable versioning on the S3 bucket nautilus-s3-3215
aws s3api put-bucket-versioning \
    --bucket nautilus-s3-3215 \
    --versioning-configuration Status=Enabled
```
```bash
# Check if versioning is enabled on the bucket
aws s3api get-bucket-versioning --bucket nautilus-s3-3215
```