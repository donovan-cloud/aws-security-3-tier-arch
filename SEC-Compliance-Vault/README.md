# Project: Automated SEC/FINRA Audit Log Vault (WORM)

## Executive Summary
This project implements a high-stakes compliance architecture for financial services environments. By leveraging **S3 Object Lock** and **AWS CloudTrail**, I've created an immutable audit trail designed to satisfy the strict record-keeping requirements of **SEC Rule 17a-4(f)** and **FINRA Rule 4511**.

## Core Architectural Guardrails
*   **WORM Storage (Write-Once-Read-Many)**: Implemented S3 Object Lock in **Compliance Mode**. Unlike Governance Mode, this setting cannot be bypassed by any user, including the Root administrator, ensuring absolute data integrity.
*   **Log File Validation**: Enabled hash-based validation in AWS CloudTrail to provide an verifiable "chain of custody" for forensic audits.
*   **Customer Managed Encryption**: Orchestrated a **Customer Managed Key (CMK)** via AWS KMS to ensure full technical sovereignty over data-at-rest.

## Proof of Implementation (Access Denied Test)
The following screenshot demonstrates a system-enforced block. Even with **Root/Admin privileges**, a permanent deletion request of a protected version is denied by the AWS S3 API, proving the immutability of the vault.
<img width="1470" height="956" alt="Screenshot 2026-05-11 at 3 49 11 PM" src="https://github.com/user-attachments/assets/01cadf14-57d6-472d-8925-a949b0cd6150" />
