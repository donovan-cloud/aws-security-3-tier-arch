# Project: Automated SEC/FINRA Audit Log Lock

## Overview
Implemented an immutable audit trail designed for SEC Rule 17a-4 compliance. This vault ensures that financial audit logs are protected by hardware-level WORM (Write Once, Read Many) storage.

## Key Features
- **Immutability**: S3 Object Lock in **Compliance Mode** prevents any user (including Root) from deleting logs.
- **Data Integrity**: CloudTrail Log File Validation ensures evidence hasn't been tampered with.
- **Encryption**: AES-256 encryption using a Customer Managed Key (CMK) in AWS KMS.

## Proof of Compliance
<img width="1470" height="956" alt="Screenshot 2026-05-11 at 3 49 11 PM" src="https://github.com/user-attachments/assets/01cadf14-57d6-472d-8925-a949b0cd6150" />
