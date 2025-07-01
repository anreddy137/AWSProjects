<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated network within the AWS cloud where you can launch and manage AWS resources like EC2 instances, databases, and load balancers. It gives you full control over your virtual network environment—including selecting your IP address range, creating subnets, configuring route tables, and setting up gateways.

VPC is useful because it lets you define how your resources communicate with each other and the internet in a secure and structured way. Without a VPC, your resources would be exposed or disorganized. With it, you can separate public and private parts of your application, apply fine-grained security rules, and meet networking and compliance requirements more easily.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create a secure, isolated network environment where I could launch my AWS resources. I started by creating a custom VPC with a defined IPv4 CIDR block, then added a subnet to organize my resources within a specific Availability Zone. I enabled auto-assign public IPv4 addresses for the subnet to ensure my instances could communicate with the internet. Finally, I created and attached an internet gateway to my VPC and updated the route table to allow internet access. This setup allowed me to build a structured, internet-connected network from scratch using Amazon VPC.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how important it is to get the CIDR blocks exactly right when creating the VPC and subnet. Even a small mistake—like choosing a subnet range that doesn’t fit within the VPC range—can lead to errors that aren’t always easy to understand at first. It showed me how precise you have to be when setting up network configurations, and how much attention to detail cloud networking requires.

### This project took me...

This project took me approximately 45 minutes to an hour. The steps were straightforward, but I spent extra time making sure the CIDR blocks were correctly configured and double-checking the subnet and route table settings. Using both the Console and CloudShell added some learning time, but it was valuable to see both approaches in action.

---

## Virtual Private Clouds (VPCs)

VPCs are Virtual Private Clouds that act like private, isolated networks within AWS where you can launch and manage your resources—like EC2 instances, databases, and more—in a secure and organized way.

They give you control over your network setup, such as assigning IP ranges, creating subnets, setting up routing, and configuring security with firewalls (called security groups and network ACLs). Without VPCs, all AWS resources would live in one big shared space, which would be chaotic and insecure. VPCs bring structure, security, and privacy—just like how neighborhoods, streets, and locked doors organize and protect homes in a city.

There was already a default VPC in my account ever since my AWS account was created. This is because AWS automatically sets up a default Virtual Private Cloud to help users get started quickly. It allows you to launch and connect core services like EC2 instances right away—without having to manually create networking infrastructure first. This default setup ensures you can use key services from Day 1, even if you haven’t learned how to configure custom VPCs yet.

To set up my VPC, I had to define an IPv4 CIDR block, which is a range of IP addresses that my VPC can use for its resources, like EC2 instances or load balancers. CIDR stands for Classless Inter-Domain Routing, and it helps define how large the network is by specifying both the starting IP address and the size of the block. For example, a CIDR block like 10.0.0.0/16 means the VPC can have up to 65,536 IP addresses, giving plenty of space to create subnets and assign IPs within the network.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are smaller networks within a VPC that allow you to organize and control how your resources are grouped and accessed. There are already subnets existing in my account, one for every Availability Zone in my selected AWS Region—thanks to the default VPC that AWS automatically created for me.

Each subnet resides in a single Availability Zone and has its own unique range of IP addresses. Subnets help define whether resources are publicly accessible (public subnets) or isolated from the internet (private subnets), giving you more control over your network's architecture and security.

Once I created my subnet, I enabled auto-assign public IPv4 addresses. This setting makes sure that any new resource, like an EC2 instance launched in that subnet, automatically gets a public IP address so that it can communicate with the internet. Without this setting, resources would only get private IPs, meaning they’d be isolated from the public internet unless manually assigned a public IP or routed through a NAT gateway.

The difference between public and private subnets are based on whether the resources inside them can directly access the internet. For a subnet to be considered public, it has to be associated with a route table that has a route pointing to an internet gateway. Without that route, even if the subnet exists in a VPC with an internet gateway, its resources can't reach the internet and the subnet is treated as private.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

Internet gateways are virtual devices in AWS that connect your VPC to the public internet. They act like a bridge, allowing resources in your VPC—such as EC2 instances in public subnets—to send and receive data from the internet. Without an internet gateway, your VPC remains isolated, meaning resources inside it can't communicate with anything outside unless routed through other services like VPNs or Direct Connect.

Attaching an internet gateway to a VPC means the resources inside public subnets of that VPC can access the internet and be accessed from the internet, provided the route tables and IP settings are correctly configured. If I missed this step, even if my subnet is labeled as public and my instances have public IPs, they still wouldn't be able to connect to the internet—because there's no actual path for network traffic to leave or enter the VPC.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources could also be created with CloudShell, which is a browser-based command-line environment provided by AWS that gives you instant access to the AWS CLI without needing to install anything locally. CLI is the Command Line Interface, a tool that lets you interact with AWS services by typing commands, making it a powerful way to automate tasks, script deployments, and manage resources efficiently—especially for repeatable or large-scale operations.

To set up a VPC or a subnet, you can use the command aws ec2 create-vpc or aws ec2 create-subnet. Make sure to avoid errors by including a correctly formatted CIDR block—for example, something like 10.0.0.0/16 for the VPC. If you're creating a subnet, its CIDR block must fall entirely within the VPC's range, such as 10.0.1.0/24. A common mistake is using a subnet block that’s too large or doesn’t fit inside the VPC's block. Also, the number after the slash in the subnet’s CIDR block should be larger than the one in the VPC’s block, since the subnet must be a smaller segment. Errors can also happen if your CIDR block has formatting issues like extra dots or missing numbers. All of these things can cause your command to fail, so it’s important to carefully check the details.

Compared to using the AWS Console, an advantage of using commands is that it's faster and more efficient once you know the syntax—you can automate repetitive tasks and set up resources with just a few lines. An advantage of using the Console is that it's more visual and beginner-friendly, making it easier to understand what's happening step by step, especially when you're still learning. Overall, I preferred using the Console at first because it helped me see and understand the structure of my VPC setup more clearly, but I can see how the CLI becomes more powerful for real-world projects and automation.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-vpc_9b2465411)

---

---
