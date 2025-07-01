<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a logically isolated network within the AWS Cloud where you can launch and manage AWS resources securely. It’s useful because it gives you full control over your network settings, such as IP address ranges, subnets (public and private), route tables, internet gateways, NAT gateways, security groups, and network ACLs.

With Amazon VPC, you can design a cloud network that mirrors a traditional on-premises setup while benefiting from AWS scalability, flexibility, and security. It's the foundation for securely hosting applications, databases, and services in the cloud.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to quickly launch a complete network environment using the “VPC and more” option. This allowed me to set up:

A new VPC with a defined CIDR block

One public and one private subnet, each with unique IP ranges

An internet gateway for public internet access

Separate route tables for the public and private subnets

And optional NAT gateway settings (which I skipped to avoid charges)

I also explored the VPC resource map, which gave a clear visual of how everything was connected. It made creating and understanding my VPC architecture much faster and easier.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how intuitive and visual the VPC resource map was. I thought setting up a full network architecture would still require switching between multiple pages, but the “VPC and more” option streamlined everything onto one screen. It was surprising (and awesome) to see how easily I could visualize and configure subnets, route tables, and gateways all in one place.

### This project took me...

This project took me approximately 20 to 30 minutes. Using the “VPC and more” setup streamlined the process significantly, saving time compared to the manual approach. Most of the time was spent reviewing the resource map, configuring CIDR blocks, and understanding how all the components connected together. It was a quick and efficient way to launch a fully functional VPC!

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means connecting to the EC2 instance’s operating system using a secure method like SSH, allowing you to interact with it as if you were physically using the machine. This lets you run commands, install software, edit files, and configure services from the inside. It’s useful for performing administrative tasks, troubleshooting issues, or deploying applications directly on the instance.

### SSH is a key method for directly accessing a VM

SSH traffic means a secure communication protocol used to remotely access and manage another machine over a network. It encrypts all data exchanged between your computer and the remote server—such as login credentials, commands, and responses—ensuring confidentiality and integrity. In this project, SSH traffic allows the public EC2 instance to securely connect to the private EC2 instance without exposing it directly to the internet.

### To enable direct access, I set up key pairs

Key pairs are a set of secure cryptographic keys used to authenticate access to your EC2 instances. They consist of two parts: a public key and a private key. The public key is stored on your EC2 instance, and the private key is downloaded and kept securely by you.

When you connect to your EC2 instance (for example, via SSH), AWS uses this key pair mechanism to verify your identity. Only someone with the correct private key can successfully decrypt the authentication request and gain access, making key pairs an essential security tool for direct access to virtual machines in AWS.

A private key's file format means the type of encoding used to save the private key on your local machine, which determines how it can be used or imported by SSH clients or other tools.
My private key's file format was .pem (Privacy Enhanced Mail), which is the standard format used for RSA keys in AWS and is required for SSH access from most terminals.

---

## Launching a public server

I had to change my EC2 instance's networking settings by associating it with the correct public subnet, linking it to the appropriate security group that allows HTTP and SSH access, and ensuring it had a public IPv4 address assigned. These steps made sure the instance could communicate over the internet and be accessed securely for administrative tasks. 

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because it has different access requirements compared to the public server. While the public server needs to allow inbound traffic from the internet (like HTTP or SSH from anywhere), the private server should only accept traffic from trusted sources—like the public server or other internal resources. This separation improves security by ensuring the private server is not directly exposed to the internet and only allows controlled, specific communication.

My private server's security group's source is NextWork Public Security Group, which means only instances within that public security group—like my public EC2 instance—are allowed to initiate connections to the private server. This setup ensures secure, internal communication between the two instances while keeping the private server isolated from direct internet access.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I selected the "VPC and more" option in the VPC console, which launched the VPC resource map—a visual tool that let me create all core VPC components in a single flow. I defined the number of Availability Zones, set up one public and one private subnet with unique CIDR blocks (10.0.0.0/24 and 10.0.1.0/24), and chose not to create a NAT gateway to avoid extra costs. This method was much faster and more intuitive, giving me a full VPC architecture with just a few clicks.

A VPC resource map is a visual representation of your VPC's architecture that shows how resources like subnets, route tables, internet gateways, and NAT gateways are connected. It helps you quickly understand the structure and flow of your network setup, making it easier to identify which subnets are public or private, how routing is configured, and how traffic moves within your VPC. It’s especially useful when creating a VPC using the “VPC and more” option, as it simplifies setup and improves visibility into your network design.

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because each VPC is logically isolated from the others within AWS by default. This means they don’t interact or route traffic between each other unless explicitly connected using features like VPC peering or Transit Gateway. Since there's no automatic communication between VPCs, overlapping CIDR blocks won't cause conflicts unless those VPCs are linked.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: 0 or 2. This was because the VPC setup wizard was distributing one public subnet per Availability Zone, and I had selected 2 Availability Zones. The tool is designed to create highly available architectures by default, so it auto-generates one public subnet per AZ to support redundancy and fault tolerance.

The set up page also offered to create NAT gateways, which are network devices that allow instances in a private subnet to connect to the internet or other AWS services, without allowing inbound traffic from the internet back into those instances. NAT stands for Network Address Translation. These gateways are useful when private instances need to download updates or communicate externally in a secure way. However, they come with additional costs—so for this project, I chose not to create one to keep things budget-friendly.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-ec2_8ee57662)

---

---
