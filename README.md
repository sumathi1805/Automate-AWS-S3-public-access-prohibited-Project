# Automate-AWS-S3-public-access-prohibited-Project
## Description
This project implement an automated remedian workflow to protect S3 bucket which is from public exposure.
## Services
* S3 
* Lambda
* IAM Role
* AWS Config
* AWS Eventbridge
* SNS

![Automate-s3-public-access-prohibited-project](https://github.com/user-attachments/assets/15c499d1-fc6b-41c3-a6b9-8b5fe47162c5)

## STEP 1: S3 setup
* Created a new S3 bucket with  block public access 'disabled' to allow public access at bucket level.
* Confidured object-level ACL to grant read access to everyone within the bucket.
## STEP 2: AWS Config monitoring
* Implemented AWS config used to continously capture changes in S3 services.
* Configured AWS config managed rule **"s3-bucket-level-public-access-prohibited"** used to detect buckets with public access and which is automatically flagged as **"NON-COMPLIANT"**.
## STEP 3: SNS
* Created SNS topic and subscription
* Integrated SNS to notify security team after each remediation.
* Messages includes bucket and remediation status.
## STEP 4: AWS Lambda Remediation
* Developed an AWS Lambda function to automatically block public access at the bucket level and update object ACLs to private.
* Configured the **SNS Topic ARN** as an **environment variable** to enable automated notifications.
* Assigned all necessary **IAM permissions**, including:
          * Blocking bucket-level public access
          * Updating object ACLs
          * Publishing to SNS
          * Default Lambda execution permissions
## STEP 5: Eventbridge Automation
* Config compliance change events were forwarded to Amazon EventBridge.
* An EventBridge rule was created to capture NON_COMPLIANT events for S3 buckets and trigger Lambda remediation.
