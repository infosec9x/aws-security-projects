<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** Abel Omambia  
**Email:** abelomambia55@gmail.com

---

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project, we will demonstrate how to use AWS Secrets Manager for secure credentials management. We're doing this project to learn how to protect our credentials when we connect live (in production) apps to our AWS environment and databases etc.

### Tools and concepts

Services I used were AWS Secrets Manager, Git, and GitHub. Key concepts I learned include secure secret management, using Secrets Manager to replace hardcoded credentials, Git interactive rebase to remove sensitive data from commit history, and handling merge conflicts. Additionally, I reinforced best practices for collaborative coding, repository cleanup, and security in version control.

### Project reflection

This project took me approximately 3 hours to complete. The most challenging part was definitely handling the Git interactive rebase dealing with merge conflicts and making sure I didn’t accidentally break anything felt a bit nerve-wracking. But once I got the hang of it, it was a great learning experience. It was most rewarding to see my repo cleaned up and fully secure, knowing that I had successfully removed sensitive data and implemented best practices. Now, I can confidently manage secrets in a professional way without worrying about accidental exposure! 

I did this project to gain hands-on experience and deepen my knowledge, especially in AWS security practices and Git version control. I also just love working in AWS environments there’s always something new to learn, and every project feels like leveling up my skills. Plus, getting better at Git and handling real world scenarios like secret management makes me feel more confident in my workflow. This project definitely met my goals, and I had a great time tackling the challenges along the way! 

---

## Hardcoding credentials

In this project, a sample web app is exposing AWS credentials by storing them directly in the config.py file. It is unsafe to hardcode credentials because doing so makes them easily accessible to anyone who has access to the code, especially if the repository is shared publicly on GitHub.

I've set up the initial configuration with a set of Access Key ID and Secret Access Key. These credentials are just examples because using test credentials prevents exposing my actual AWS credentials while doing this project.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

As an extension of this project, I decided to run the web app locally using my own AWS credentials. To set up my virtual environment, I installed essential packages like boto3, FastAPI, and Uvicorn, which are required for the app to function. boto3 allows the app to connect to AWS services like S3, FastAPI provides the framework for building the web API, and Uvicorn serves as the ASGI server to run the application. These dependencies ensure seamless communication between the web app and AWS while enabling efficient API handling and local deployment.

When I first ran the app, I ran into an error because the AWS Access Key ID provided was not valid. The JSON response displayed {"error":"An error occurred (InvalidAccessKeyId)..."}, which means the web app attempted to authenticate with AWS using the placeholder credentials in config.py. Since these credentials are not real, the app couldn't access my AWS account or list the S3 buckets. This error highlights the importance of using valid credentials for AWS authentication and reinforces why hardcoding sensitive credentials is not a secure practice.

To resolve the 'InvalidAccessKeyId' error, I updated the config.py file with my real AWS credentials. I replaced the placeholder AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY with the actual values generated from the IAM console, ensuring the web app can authenticate with AWS. I also updated the AWS_REGION to match the region where my S3 buckets are located. These changes allow the web app to securely connect to AWS and retrieve my S3 bucket list. However, since storing credentials in a configuration file is not a secure practice, I will later migrate them to AWS Secrets Manager for better security.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_wghjteykut)

---

## Pushing Insecure Code to GitHub

Once I updated the web app code with credentials, I forked the repository because I wanted to create my own copy of the project on GitHub without modifying the original repository. A fork is different from a clone because forking creates a separate repository under my GitHub account, making it publicly accessible, while cloning only creates a local copy on my computer. By forking the repository, I can push changes, test GitHub’s secret scanning feature, and demonstrate the risks of exposing credentials in a real world scenario.

To connect my local repository to the forked repository, I first initialized Git using git init, which allowed Git to track changes in my project. Then, I set up the remote repository by running git remote set-url origin <forked-repo-url>, linking my local project to my forked GitHub repository. After verifying the connection with git remote -v, I staged my changes using git add ., which prepared all modified files for commit. I then used git commit -m "Updated config.py with hardcoded credentials" to save a snapshot of my changes in the local repository. Finally, git push -u origin main uploaded my committed changes to the main branch of my forked repository, making my code including the hardcoded credentials public on GitHub.

GitHub blocked my push because it detected AWS credentials, preventing accidental exposure. This security feature protects against unauthorized access and encourages best practices like using secret managers or environment variables.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is an AWS service that securely stores and manages sensitive information like database credentials, API keys, and authentication tokens. I'm using it to store my AWS credentials, preventing them from being hardcoded in my code and reducing security risks. Other common use cases include storing database credentials, OAuth tokens, and other sensitive configuration values while enabling automated secret rotation and auditing.

Another feature in Secrets Manager is secret rotation, which means automatically updating and replacing secrets on a set schedule to reduce the risk of compromised credentials. It's useful in situations where credentials, such as database passwords, privileged API keys, or service account credentials, need regular updates to maintain security. Secret rotation is especially important for high risk credentials that, if exposed, could grant unauthorized access to critical systems or sensitive data.

Secrets Manager provides sample code in various languages, like Python, Java, and JavaScript, to help developers easily retrieve secrets in their applications. This is helpful because it eliminates the need to hardcode credentials, reducing security risks. By using the provided code, developers can securely access secrets programmatically, ensuring seamless integration with AWS services while maintaining best practices for credential management.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the config.py file to retrieve AWS credentials securely from Secrets Manager instead of using hardcoded values. The get_secret() function will connect to AWS Secrets Manager using boto3, fetch the secret named "aws-access-key", and return the credentials. It includes error handling using a try-except block to catch potential issues like missing permissions or incorrect configurations. This approach enhances security by keeping credentials encrypted and centrally managed, reducing the risk of exposure.

I also added code to config.py to extract the AWS credentials from the retrieved secret and assign them to the AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_REGION variables. This is important because our application (app.py) expects these variables to authenticate with AWS services. The code first calls get_secret() to fetch the secret, parses it using json.loads(), and then assigns the extracted values to the appropriate variables. This ensures our credentials are securely retrieved at runtime instead of being hardcoded, improving security and maintainability.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is a process that allows you to rewrite commit history by modifying, reordering, or squashing commits. I used it to remove a commit that contained sensitive credentials by marking it with d (drop) during an interactive rebase. This was necessary because the commit had exposed AWS credentials, and simply making a new commit removing them wouldn’t erase them from the Git history. By rebasing, I ensured that the sensitive data was completely removed from the repository’s history, reducing the risk of accidental exposure.

A merge conflict occurred during rebasing because I removed the commit with hardcoded credentials, but a later commit also modified config.py. I resolved it by deleting the old hardcoded credentials, keeping the updated Secrets Manager version, and removing the conflict markers. This ensured only the secure version remained.

Once the merge conflict was resolved, I verified that my hardcoded credentials were removed by checking config.py on GitHub. I ensured that the file only contained the secure code for retrieving credentials from AWS Secrets Manager and confirmed that no sensitive information remained in the commit history.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
