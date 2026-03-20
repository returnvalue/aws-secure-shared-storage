# AWS Secure Shared Storage (Terraform)

This repository demonstrates a production-grade shared storage architecture provisioned using **Terraform**. It follows the **Secure Shared Storage Pattern**, a key requirement for the AWS Certified Solutions Architect - Associate (SAA-C03) exam.

## 🏗️ Architecture Overview

The infrastructure is designed to provide highly available, encrypted, and automatically backed-up file storage that can be shared across multiple compute instances. The architecture consists of:

1.  **Storage Layer:** An **Amazon EFS (Elastic File System)** providing a scalable, NFS-compliant file system.
2.  **Security Layer:** Data-at-rest encryption using **AWS KMS** with a Customer Managed Key (CMK) and granular **Security Group** rules for NFS traffic (Port 2049).
3.  **Connectivity Layer:** **EFS Mount Targets** distributed across multiple Availability Zones to ensure low-latency access and high availability.
4.  **Governance Layer:** An **AWS Backup** plan that automates daily snapshots with a 30-day retention policy, stored in a secure Backup Vault.

## 🛠️ SAA-C03 Design Patterns Covered

- **Design Secure Architectures (Domain 2):** 
    - **Encryption at Rest:** Uses KMS Customer Managed Keys rather than default AWS managed keys for enhanced control.
    - **Network Firewalls:** Implements "Least Privilege" security groups to restrict file system access to only authorized CIDR blocks.
- **Design Resilient Architectures (Domain 1):** Multi-AZ mount targets ensure that compute instances can access the shared data even if a single data center fails.
- **Design High-Performing Architectures (Domain 3):** EFS provides elastic throughput and performance that scales automatically with the size of the data.

## 🚀 Technical Components

- **Storage:** EFS File System with encrypted lifecycle management.
- **Security:** KMS Keys, Aliases, and NFS-specific Security Groups.
- **Governance:** AWS Backup Vaults, Backup Plans, and IAM Service Roles.
- **Networking:** Multi-AZ VPC with private subnet isolation for data integrity.
- **Infrastructure as Code:** 100% automated via Terraform with a state-managed lifecycle.

## 💻 Local Development

This project is optimized for testing using **LocalStack**.

### Prerequisites
- [Terraform](https://www.terraform.io/downloads)
- [Docker](https://www.docker.com/products/docker-desktop)
- [LocalStack](https://localstack.cloud/)

### Deployment
1. Start LocalStack: `docker compose up -d`
2. Initialize Terraform: `terraform init`
3. Deploy Infrastructure: `terraform apply -auto-approve`
