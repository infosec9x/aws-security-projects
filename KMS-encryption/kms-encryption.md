<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Abel Omambia  
**Email:** abelomambia55@gmail.com

---

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use AWS KMS to create encryption keys, encrypt a DynamoDB database, securely add and retrieve data, and grant user access, highlighting secure cloud data management.

### Tools and concepts

Services I used include DynamoDB, IAM, and KMS. Key concepts I learned include encryption, key management, access control, and secure data deletion. I practiced managing permissions, enforcing security, and properly decommissioning resources.

### Project reflection

This project took me approximately a few hours. The most challenging part was configuring KMS permissions correctly. It was most rewarding to see how encryption controls access, ensuring only authorized users can decrypt and view protected data.

I did this project today to deepen my understanding of AWS KMS encryption and access management. This project met my goals by helping me practice securing DynamoDB data, managing IAM permissions, and reinforcing best practices for cloud security.

---

## Encryption and KMS

Encryption converts plain text into unreadable ciphertext using algorithms to protect sensitive data and ensure privacy. Encryption keys guide the process and are essential for encrypting and decrypting data.

AWS KMS is a secure service for managing encryption keys to protect AWS data. Key management systems centralize storage, enhance security, and provide compliance logs.

Encryption keys are broadly categorized as symmetric and asymmetric. I chose a symmetric key because it uses a single key for encryption and decryption, making it faster and more efficient for encrypting large datasets, like our DynamoDB table.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is a fully managed NoSQL database service by AWS. It provides fast, scalable, and highly available storage, making it ideal for applications that require quick access to large datasets.

The different encryption options in DynamoDB include Amazon DynamoDB-owned keys, AWS-managed keys, and customer-managed keys (CMK). Their differences are based on control and visibility. I selected CMK for full access control and enhanced security.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by using IAM policies, key policies, and grants. These define who can encrypt, decrypt, or manage the key, ensuring only authorized users perform sensitive actions.

Despite encrypting my DynamoDB table, I could still see the table's items because I have permission to use the KMS key. DynamoDB uses transparent data encryption, meaning authorized users can access decrypted data while keeping it secure at rest.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to test KMS encryption restrictions. The permission policies I granted this user are AmazonDynamoDBFullAccess but not KMS key access. This ensures they can access DynamoDB but cannot decrypt the encrypted data.

After accessing the DynamoDB table as the test user, I encountered an access denied error because the user lacks KMS decryption permissions. This confirmed that KMS encryption blocks unauthorized access, ensuring data security at rest.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I added them as a key user in KMS. My key's policy was updated to allow actions like encrypt, decrypt, re-encrypt, generate data keys, and describe the key, ensuring controlled access to encrypted data.

To let my test user use the encryption key, I added them as a key user in KMS. My key's policy was updated to allow actions like encrypt, decrypt, re-encrypt, generate data keys, and describe the key, ensuring controlled access to encrypted data.

Encryption secures data instead of just restricting access. I could combine it with IAM policies and security groups to control access while ensuring only authorized users with the decryption key can read the data.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-kms_feffb2fb8)

---

---
