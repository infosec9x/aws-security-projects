<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-iam)

**Author:** Abel Omambia  
**Email:** abelomambia55@gmail.com

---

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Tools and concepts

AWS Identity and Access Management (IAM) secures AWS resources by managing users, roles, and permissions. It enforces least privilege, supports MFA, and enables centralized management, temporary access, and compliance auditing.

### Project reflection

I used AWS IAM to create and test a user with limited permissions, ensuring access to the development instance while restricting production access, following the principle of least privilege.

---

## Tags

Tags are key-value pairs that help organize, manage, track costs, automate actions, control access, and ensure compliance for AWS resources.

The tag I’ve used is Env and Name, with values production/nextwork-production-aomambia1234 and development/nextwork-development-aomambia1234

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

IAM Policies are rules that define permissions for who can access AWS resources, what actions they can perform, and under what conditions, ensuring secure and controlled resource management.

### The policy I set up

For this project, I’ve set up a policy using the JSON editor, which provides precise control over the permissions assigned to the intern for the development EC2 instance.

I’ve created a policy that allows the intern to start, stop, and describe EC2 instances tagged with Env = development while denying the ability to create or delete tags on all instances. This ensures the intern can only interact with the development 

### When creating a JSON policy, you have to define its Effect, Action and Resource.

The Effect, Action, and Resource attributes of a JSON policy mean whether an action is allowed or denied (Effect), what operations are allowed (Action), and which AWS resources it applies to, like specific instances or all resources (Resource).

---

## My JSON Policy

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_1c864649)

---

## Account Alias

An account alias is a user-friendly name for your AWS account, replacing the default account ID in the sign-in URL to make it easier to remember and share.

Creating an account alias took me just a few minutes. Now, my new AWS console sign-in URL is: https://nextwork-alias-aomambia1234.signin.aws.amazon.com/console

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### Users

IAM users are individual accounts created within AWS to provide specific people or applications access to AWS resources, with permissions managed independently or via user groups.

### User Groups

IAM user groups are collections of IAM users that allow you to manage permissions collectively by attaching policies to the group, rather than assigning them to individual users.

I attached the policy I created to this user group, which means all users in the group automatically inherit the permissions defined in the policy, ensuring consistent access control for all interns.

---

## Logging in as an IAM User

The first way is by sharing the AWS sign-in URL, username, and password securely.The second way is by securely sharing the downloaded credentials file.

Once I logged in as my IAM user, I noticed "Access Denied" on some panels because the user's permissions were limited to the development instance, restricting access to other resources like the production instance.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

I tested my JSON IAM policy by attempting to stop and restart the two EC2 instances assigned to my environment. This process validated whether the IAM policy applied the appropriate permissions to manage the instance states.

### Stopping the production instance

When I tried to stop the production instance, I received an error stating I was not authorized. This was because the IAM user’s permissions are restricted to the development instance and explicitly deny actions on instances with the production tag.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_0e7a9d6a)

---

## Testing IAM Policies

### Stopping the development instance

Next, when I tried to stop the development instance, the operation succeeded, and the instance transitioned to a stopped state. This occurred because my IAM policy explicitly permitted the "StopInstances" action, ensuring proper access.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-iam_1811801c)

---

## The IAM Policy Simulator

### How I used the simulator

---

---
