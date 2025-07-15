<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Threat Detection with GuardDuty

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-guardduty)

**Author:** Abel Omambia  
**Email:** abelomambia55@gmail.com

---

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_sm42x3y4)

---

## Introducing Today's Project!

### Tools and concepts

The services I used were AWS CloudFormation, Amazon S3, Amazon EC2, AWS CloudShell, and Amazon GuardDuty. Key concepts I learned include threat detection, SQL injection, credential theft, and malware protection in AWS.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was configuring the AWS CLI with stolen credentials. It was most rewarding to see GuardDuty detect threats, confirming my understanding of AWS security monitoring.

I did this project to gain hands-on experience with AWS security tools, especially GuardDuty, to improve my threat detection skills. It met my goals by helping me simulate attacks and understand how GuardDuty detects threats.

---

## Project Setup

To set up for this project, I deployed a CloudFormation template that launches a vulnerable web app. The three main components are: an EC2 instance with OWASP Juice Shop, an S3 bucket for sensitive data, and GuardDuty for threat detection.

The web app deployed is called OWASP Juice Shop. To practice my GuardDuty skills, I will simulate cyberattacks by exploiting its vulnerabilities, steal sensitive data, and analyze how GuardDuty detects and reports these threats.

GuardDuty is an AWS threat detection service using machine learning to spot security risks. In this project, it will monitor the web app, detect attacks, and generate alerts for threat analysis.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_n1o2p3q4)

---

## SQL Injection

The first attack I performed on the web app is SQL injection, which means inserting malicious SQL code into database queries to manipulate them. SQL injection is a security risk because it can bypass authentication and expose sensitive data.

My SQL injection attack involved entering ' OR 1=1;-- into the login field. This means I manipulated the SQL query to always return true, bypassing authentication and gaining unauthorized access to the web app.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_h1i2j3k4)

---

## Command Injection

Next, I used command injection, which is a vulnerability that lets attackers execute malicious commands on a server via input fields. The Juice Shop web app is vulnerable because it doesn’t sanitize user input, allowing harmful code execution.

To run command injection, I entered malicious JavaScript into the username field of the admin profile. The script will trick the server into executing commands to steal AWS IAM credentials and save them in a public JSON file.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_t3u4v5w6)

---

## Attack Verification

To verify the attack's success, I accessed [JuiceShopURL]/assets/public/credentials.json, where the stolen credentials were saved. The page showed AWS access keys, secret keys, and session tokens, confirming the attack worked.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_x7y8z9a0)

---

## Using CloudShell for Advanced Attacks

The attack continues in CloudShell because it lets me simulate a hacker using stolen credentials to access my AWS environment. Since CloudShell uses a different account ID, the activity appears suspicious to GuardDuty, triggering threat detection.

In CloudShell, I used wget to download the stolen credentials.json file from the web app to my CloudShell environment. Next, I ran cat and jq to display and format the JSON data, making the AWS credentials easy to read.

I then set up a profile, called stolen, to use the stolen AWS credentials and simulate unauthorized access to my AWS environment. I had to create a new profile because it lets me act as a hacker without using my default permissions.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_j9k0l1m2)

---

## GuardDuty's Findings

After performing the attack, GuardDuty reported a finding within 15 minutes. Findings are alerts that identify suspicious activities in your AWS environment, detailing what happened, who did it, and how it occurred for incident response.

GuardDuty's finding was called UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS, which means stolen EC2 credentials were used within AWS by another account. Anomaly detection flagged this unusual activity as a threat.

GuardDuty's detailed finding reported that stolen IAM credentials were used to access my Juice Shop's S3 bucket. It showed the affected resource was an IAM role, the action was object retrieval, and included the attacker’s IP and location.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_v1w2x3y4)

---

## Extra: Malware Protection

For my project extension, I enabled Malware Protection for S3 in GuardDuty. Malware is harmful software designed to damage systems, steal data, or disrupt operations. This feature helps detect and prevent malware threats in AWS.

To test Malware Protection, I uploaded an EICAR test file to my S3 bucket. The uploaded file won't cause damage because it’s a harmless file designed to trigger security tools like GuardDuty for testing malware detection.

Once I uploaded the file, GuardDuty instantly triggered a finding called Object:S3/MaliciousFile. This verified that GuardDuty’s Malware Protection effectively detected the test malware, confirming it can identify threats in S3 buckets.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-guardduty_sm42x3y4)

---
