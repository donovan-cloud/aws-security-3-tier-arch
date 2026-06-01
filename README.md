# Enterprise-Grade Security-Hardened 3-Tier AWS Architecture

## 📌 Architectural Overview
This repository contains the design standards and infrastructure blueprints for a production-ready, zero-trust 3-tier web architecture natively built on AWS. The design strictly enforces the principle of least privilege, complete logical tier isolation, and defense-in-depth methodologies to secure enterprise workloads from edge vulnerabilities down to the database storage layer.

---

## 🛡️ Core Security Blueprint & Traffic Isolation

The infrastructure is distributed across multiple Availability Zones (AZs) for high availability and leverages isolated Virtual Private Cloud (VPC) subnets to prevent lateral movement in the event of a tier compromise:

### 1. Presentation Tier (Public Subnets)
* **Components:** Public-facing Application Load Balancers (ALB).
* **Ingress Control:** Stripped down to accept only HTTPS (Port 443) traffic originating from verified internet gateways.
* **Security Posture:** Acts as the isolated perimeter layer; no application logic or business data resides here.

### 2. Application Tier (Private Subnets)
* **Components:** Private EC2 Application Instances / Auto Scaling Groups.
* **Ingress Control:** Inbound traffic is strictly locked down via Security Groups to *only* accept requests routed from the Presentation Tier ALB. 
* **Egress Control:** Direct internet routing is entirely blocked. Outbound updates or API calls are channeled securely through highly available NAT Gateways.

### 3. Data Tier (Isolated Private Subnets)
* **Components:** Amazon RDS Multi-AZ Database Clusters.
* **Ingress Control:** The strictest layer in the architecture. Security Group ingress rules explicitly deny all traffic except native database queries (e.g., Port 3306/5432) originating exclusively from the private Application Tier EC2 instances.
* **Isolation Posture:** Complete logical detachment from the public internet—zero direct ingress or egress routing allowed.

---

## 🔒 Threat Modeling & Risk Mitigation

| Attack Vector | Architectural Mitigation Strategy |
| :--- | :--- |
| **Public Internet Exposure** | Application servers and database clusters are housed in non-routable private subnets using private RFC 1918 IP spacing. |
| **Lateral Movement** | Statefully controlled state-tracking Security Groups act as micro-firewalls around every single component, rejecting all non-scoped traffic. |
| **Single Point of Failure** | Implemented multi-AZ component distribution paired with automated health checks to guarantee fault tolerance and high availability. |
| **Data At-Rest Compromise** | Storage volumes across the application instances and RDS instances are encrypted using industry-standard AES-256 via custom AWS KMS keys. |

---

## 📊 Business Value & Compliance Alignment
* **FinTech Compliance Baseline:** Aligns directly with network segmentation requirements outlined in **PCI-DSS Requirement 1** and **SOC 2 Type II** trust principles.
* **Blast Radius Reduction:** Micro-segmentation guarantees that a vulnerability exploitation at the web server layer cannot directly interface with or exfiltrate backend financial data stores.
