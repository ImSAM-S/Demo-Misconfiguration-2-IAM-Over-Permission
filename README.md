# Demo-Misconfiguration-2-IAM-Over-Permission
## 📌 Introduction

This project demonstrates a common AWS IAM misconfiguration: granting overly broad permissions to a user.
The goal is to highlight the risks of attaching the AdministratorAccess policy to a user instead of following the Principle of Least Privilege.

## Analyze the Issue You Will Made
Violation of Least Privilege: the user has full administrative rights instead of only the required permissions.
Security Risk: if the developer-test account is compromised, an attacker gains complete control over the AWS environment.

Potential Impact:
.Exposure of sensitive data.
.Unauthorized configuration changes.
.Creation of backdoor IAM roles.
.Deletion of services, leading to downtime.

## ⚙️ Steps to Reproduce
### 1. Creat a IAM User with AdministratorAccess plolicy

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/2b31a19efdf593cb08ef8c2772a574d368135570/01_Creat_a_new_user.png)

Complete the user creation.

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/2b31a19efdf593cb08ef8c2772a574d368135570/02_policy.png)

### 2. CLI Connected (If you use window can skip this)
Turn on your linux's terminal and connect to IAM user by write this:
                     `aws configure`
If you successed with the keys you got in IAM account and got into aws. You can use this to confrim:
                      ` aws sts get-caller-identity `
### 3. Creating bucket
With GUI: You sreach bucket on aws and create











AWS-Demo-Misconfiguration-1:S3-Public-Bucket/
├── 01_Start_to_creat_Bucket.png
├── 02_Bucket_public_settings.png
├── 03_Upload_file.png
├── 04_Bucket_policy_public.png
├── 05_Everyone_access_browser.png
├── 06_Bucket_policy_removed.png
├── 07_Get_access_denied.png
├── 08_Last_view_bucket.png
├── README.md
└── secret.txt
