# Demo Misconfiguration 2: IAM Over-Permission
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
With GUI: You search bucket on aws and create
With CLI: You use this code:

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/59fa6142604185601a9e8d2e0bae0d1388b10414/03_create_bucket.png)

Done:

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/04_Bucket_created.png)

### 4. Upload file

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/05_Upload_data.png)

### 5. See buckets
Now! You can you that IAM user account not root account to see all code beacause it has AdministratorAccess policy
I will show it on CLI:

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/06_Look_on_CLI.png)

### 6. The Things Attacker Can Do
In many cases, an attacker could perform actions such as: having admin privileges to delete data, creating a backdoor by generating an admin role and attaching it to EC2/Lambda, etc. In my demo, I will only focus on the data deletion scenario.

You are now in that IAM User account so you can remove data because you knew all info data in system

Example on CLI I will write:       `aws s3 rb s3://demo-bucket-test-1772418412 --force `

And look result

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/07_bucket_removed.png)

Yea... Our bucket we made, it has been removed

### 7. Remediation
Remove the AdministratorAccess policy from the developer-test user.

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/08_Policy_removed.png)

Create a custom policy in IAM user with only the necessary permissions, for example, read-only access to S3:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::project-misconfig-demo",
        "arn:aws:s3:::project-misconfig-demo/*"
      ]
    }
  ]
}

```

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/09_Custom_policy.png)

### 8.Check it
You can go to AWS to check it. I will use CLI:

![image alt](https://github.com/ImSAM-S/Demo-Misconfiguration-2-IAM-Over-Permission/blob/09d61b94598ddbc96009a03a085325ab6ec519fd/10_Success.png)

SUCCESS!!!

## Learned From Project
. Over-permissioning IAM users violates the Principle of Least Privilege
. AdministratorAccess attached to a user creates a high-risk scenario if compromised
. Misconfigurations can lead to full environment takeover

## Project Files
```tree
project-IAM-Over-Permission/
├── 01_Create_a_new_user.png
├── 02_policy.png
├── 03_create_bucket.png
├── 04_Bucket_created.png
├── 05_Upload_data.png
├── 06_Look_on_CLI.png
├── 07_bucket_removed.png
├── 08_Policy_removed.png
├── 09_Custom_policy.png
├── 10_Success.png
├── README.md
└── test.txt
```

## Author
ImSAM-S
