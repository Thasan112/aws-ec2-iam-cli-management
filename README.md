# aws-ec2-iam-cli-management
# AWS Cloud Administration: EC2 Bastion Connection, CLI Configuration &amp; IAM Policy Retrieval


## 📋 Overview
This project demonstrates foundational AWS cloud administration and command-line interface (CLI) operations. 
The lab covers secure remote connection to a Red Hat Enterprise Linux (RHEL) EC2 instance acting as a bastion host, manual installation and configuration of the AWS CLI, and advanced programmatic inspection and extraction of IAM security policies.


[IAM Configuration Overview](IAM.png)
---

## 🛠️ Lab Architecture & Tasks

### Task 1: Connect to the Red Hat EC2 Instance via SSH
* **Objective:** Establish a secure shell connection to a cloud-hosted RHEL virtual machine.
* **Execution:** Utilized SSH with proper private key permissions (`chmod 400`) to connect safely to the remote instance.

### Task 2: Install the AWS CLI on Red Hat Linux
* **Objective:** Prepare the Linux environment by installing prerequisites (such as Python and unzip utilities) and deploying the standalone AWS CLI bundle.
* **Verification:** Confirmed successful installation by checking the version (`aws --version`).

### Task 3 & 5: Observe IAM Configuration via Console & CLI
* **Objective:** Analyze identity and access management (IAM) permissions assigned to the lab user (`awsstudent`).
* **Execution:** Inspected user permissions natively through the AWS Management Console and subsequently validated credentials via terminal commands (`aws sts get-caller-identity`).

### Task 4: Configure the AWS CLI
* **Objective:** Securely configure local AWS credentials (`aws configure`) using ephemeral Access Key IDs, Secret Access Keys, target region (e.g., `us-east-1` / `eu-west-2`), and output formatting (`json`).

---

## 🚀 Programmatic IAM Policy Extraction

### Challenge Description
The goal was to download the specific `lab_policy` JSON-formatted IAM policy document directly to the Red Hat instance using **only the AWS CLI**, completely bypassing the AWS Management Console. 

### Step-by-Step Solution Breakdown

1. **List Policies and Filter by Scope:**
   Query the IAM service to locate the specific ARN (Amazon Resource Name) associated with the `lab_policy` using local scoping:
   ```bash
   aws iam list-policies --scope Local
