# Logically Air-Gapped Ransomware Recovery Vault

## Strategic Objective
To design and implement a ransomware-resilient backup architecture that survives a "Total Account Compromise" scenario. This solution utilizes **AWS Backup Logically Air-Gapped Vaults** to provide an immutable, isolated recovery point for mission-critical data.

## Architectural Security Controls
*   **WORM Enforcement (Compliance Mode)**: Leveraged **AWS Backup Vault Lock** in **Compliance Mode** to enforce a mandatory 7-day retention floor. No user (including Root) can delete data during the cooling-off period.
*   **Logical Air-Gapping**: Recovery points are stored in a specialized AWS-managed domain, providing a security boundary that is physically and logically separated from the primary workload account.
*   **Identity Isolation**: The recovery environment utilizes service-managed encryption to maintain a distinct security perimeter from the primary management identity.

## Proof of Implementation (Access Denied Test)
The following screenshot demonstrates a system-enforced block. Even with **Root/Admin privileges**, the 'Delete' operation is programmatically disabled by the AWS Backup API.

![Access Denied Proof](access_denied_screenshot.png)
*Figure 1: Architectural denial of a manual deletion request on a compliant object.*
