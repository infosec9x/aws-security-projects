<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Abel Omambia  
**Email:** abelomambia55@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a secure, isolated cloud network within AWS that allows users to customize their networking environment by defining IP address ranges, subnets, route tables, and gateways. It enhances security and isolation by keeping resources private unless explicitly exposed, while customizable networking enables public and private subnet configurations for efficient traffic control. VPC supports scalability and flexibility, allowing hybrid cloud setups, VPN connections, and VPC peering. With high availability and redundancy across multiple Availability Zones, it ensures resilience for critical applications. Overall, Amazon VPC is essential for building secure, scalable, and highly available cloud architectures. 

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure and isolated network for my AWS resources. First, I created a VPC with a defined IP address range (CIDR block) to establish my virtual networking environment. Then, I added subnets, dividing the VPC into smaller network segments, ensuring proper organization of resources. To enable external connectivity, I set up an internet gateway and attached it to my VPC, allowing resources in public subnets to access and be accessed from the internet. I also enabled auto assign public IP addresses for instances in the public subnet, ensuring seamless internet communication. Additionally, I used AWS CloudShell and CLI commands to automate VPC resource creation, making the process faster and more efficient. Finally, I verified the setup by checking network connections and troubleshooting dependencies before successfully deleting the VPC and its associated resources. 

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was the DependencyViolation error when trying to delete the VPC. I initially thought that deleting the VPC would automatically remove all associated resources, but I quickly realized that subnets, internet gateways, and other dependencies had to be manually deleted first. This taught me the importance of understanding resource relationships in AWS and ensuring a proper cleanup process. It was a great hands-on learning experience in troubleshooting and managing cloud infrastructure!

### This project took me...

This project took me about 1 to 2 hours, mostly because I was figuring things out as I went. Setting up the VPC, subnets, and internet gateway through the AWS Console was pretty straightforward, but using AWS CloudShell and CLI took a little longer since I had to double-check commands and troubleshoot errors. The DependencyViolation error when deleting the VPC definitely slowed things down because I had to manually remove subnets and the internet gateway first. Overall, it was a solid learning experience, and now I feel way more comfortable working with VPCs in AWS! 

---

## Virtual Private Clouds (VPCs)

VPCs are Virtual Private Clouds that create a secure, isolated network within AWS, allowing you to control how resources communicate. Without VPCs, all AWS resources would exist in a shared, open network, making security and management difficult.

There was already a default VPC in my account ever since my AWS account was created because AWS automatically provisions one for every new account. This allows users to launch resources like EC2 instances and connect services without manually setting up a VPC. It provides a ready-to-use private network, making it easier for beginners to get started, but users can always create custom VPCs for enhanced security, organization, and control over network configurations.

To set up my VPC, I had to define an IPv4 CIDR block, which is a way of allocating a range of IP addresses within my network. CIDR (Classless Inter-Domain Routing) helps determine the size of the address space by specifying how many bits of the IP address are fixed and how many can vary. For example, choosing 10.0.0.0/16 means the first 16 bits (10.0) remain constant, while the remaining 16 bits allow for 65,536 possible IP addresses within the VPC. This ensures efficient IP management, allowing resources to communicate securely within a structured private network.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are subdivisions of a VPC that organize resources based on access rules, similar to neighborhoods in a city. Public subnets allow internet access, while private subnets restrict access for security. There are already subnets in my account, one for each Availability Zone in my Region, because AWS automatically creates them in the default VPC to ensure resources are distributed for high availability. By creating custom subnets, I can control resource interactions, improve security, and optimize network management within my VPC.

Once I created my subnet, I enabled auto-assign public IPv4 addresses to ensure that any EC2 instance launched within the subnet automatically receives a public IP address. This setting makes sure that instances can immediately communicate with the internet without requiring manual IP assignment, saving time and simplifying network configuration. By enabling this option, I can seamlessly launch public-facing resources, such as web servers, so that they are accessible from external networks right away.

The difference between public and private subnets is that public subnets are connected to the internet, allowing resources inside them to communicate externally, while private subnets do not have direct internet access and are used for internal resources. For a subnet to be considered public, it has to be connected to an internet gateway, which enables outbound and inbound internet traffic. Although my subnet is labeled Public 1, it is not yet a public subnet because it still lacks this internet gateway connection. Once attached, resources inside the subnet will be able to communicate with external networks, making it truly public.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

Internet gateways are network components that connect a VPC to the internet, enabling communication between resources inside the VPC and external networks. They act as a bridge, allowing instances in public subnets to send and receive traffic from the internet. Without an internet gateway, resources within a VPC would remain isolated, unable to access external services or be accessed by users. By attaching an internet gateway to a VPC, applications and services hosted within public subnets can function as publicly accessible web servers, APIs, or other internet-facing systems.

Attaching an internet gateway to a VPC means that resources within the VPC can now communicate with the internet. This allows EC2 instances with public IP addresses to send and receive traffic from external networks, making applications hosted on those instances publicly accessible. If I missed this step, my public facing resources, such as web servers, would remain isolated within the VPC, unable to connect to the internet or serve users. The internet gateway acts as a crucial bridge, ensuring that my cloud based applications can function online as intended.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources could also be created with CloudShell, which is a built-in shell environment in the AWS Management Console that allows users to run commands without needing to install anything on their local machine. It provides a pre-configured terminal with AWS CLI and other essential tools, making it convenient for managing AWS resources directly from the browser.

CLI (Command Line Interface) is a tool that enables users to interact with AWS services using text-based commands instead of navigating through the AWS Management Console. With CLI, tasks such as creating, updating, and deleting resources can be automated, making cloud management faster and more efficient. Using AWS CloudShell with CLI streamlines infrastructure deployment, allowing engineers to set up VPCs, subnets, and internet gateways with simple commands instead of manually configuring them through the UI.

To set up a VPC or a subnet, you can use the aws ec2 create-vpc and aws ec2 create-subnet commands, but errors occur if required parameters are missing. To avoid issues, always include the --cidr-block parameter when creating a subnet, ensuring that its IP range falls within the VPC’s CIDR block. The subnet’s CIDR block must be a subset of the VPC’s, meaning it should have a larger number after the slash (e.g., /25 to /32) to fit correctly. Additionally, proper CIDR formatting is essential to prevent command failures.

Compared to using the AWS Console, an advantage of using commands is speed and automation—the AWS CLI allows for quick resource creation without manually navigating through the UI, making it ideal for scripting and repeatable deployments. An advantage of using the Console is visual clarity and ease of use, as it provides an intuitive interface where users can see and configure resources step by step without needing to remember CLI syntax. Overall, I preferred the CLI for efficiency and automation, but the Console remains useful for visual confirmation and troubleshooting, especially when learning AWS networking concepts.

![Image](http://learn.nextwork.org/serene_magenta_silly_cobra/uploads/aws-networks-vpc_9b2465411)

---

---
