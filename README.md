# Automate-AWS-S3-public-access-prohibited-Project
## Overview
This project automatically detects and remediates publicly accessible S3 buckets using AWS Config, EventBridge, Lambda, and SNS.

When a bucket becomes publicly accessible, it is flagged as **NON_COMPLIANT**, and an automated workflow removes public access and notifies the security team.

## Technologies Used
* S3 
* Lambda
* IAM 
* AWS Config
* AWS Eventbridge
* SNS

## Architecture Workflow

1. S3 bucket becomes public  
2. AWS Config detects non-compliance  
3. EventBridge triggers Lambda  
4. Lambda removes public access  
5. SNS sends notification  


![Automate-s3-public-access-prohibited-project](https://github.com/user-attachments/assets/15c499d1-fc6b-41c3-a6b9-8b5fe47162c5)

## Implementation Steps

### 🔹 Step 1: S3 Setup
- Created an S3 bucket with public access enabled (for testing)
- Configured object-level ACL to allow public read access

### 🔹 Step 2: AWS Config Monitoring
- Enabled AWS Config to track S3 changes
- Used managed rule:
  - `s3-bucket-level-public-access-prohibited`
- Buckets with public access flagged as **NON_COMPLIANT**

### 🔹 Step 3: SNS Notification
- Created SNS topic and subscription
- Configured notifications for remediation events
- Alerts include bucket name and remediation status
  
### 🔹 Step 4: Lambda Remediation
- Developed Lambda function to:
  - Block public access at bucket level
  - Update object ACLs to private
- Used environment variable for SNS Topic ARN
- Assigned IAM permissions:
  - S3 access control
  - SNS publish
  - Lambda execution role

### 🔹 Step 5: EventBridge Automation
- Forwarded AWS Config compliance events to EventBridge
- Created rule to detect **NON_COMPLIANT** S3 buckets
- Triggered Lambda automatically for remediation

## Key Features
- Automated detection of public S3 buckets
- Real-time remediation using Lambda
- Event-driven architecture using EventBridge
- Security alerts via SNS
- Fully serverless solution

## Outcome
This project ensures that no S3 bucket remains publicly accessible by automatically enforcing security policies and notifying stakeholders in real time.

## ⚠️ Challenges & Learnings

### Challenges
- Faced IAM permission issues while allowing Lambda to modify S3 bucket policies and object ACLs
- Initially struggled to correctly capture NON_COMPLIANT events from AWS Config in EventBridge
- Ensuring proper sequencing between detection (Config) and remediation (Lambda)

### Learnings
- Gained hands-on experience with event-driven architecture using AWS Config and EventBridge
- Learned how to enforce security compliance automatically using Lambda
- Improved understanding of S3 access control (bucket policies vs ACLs)
