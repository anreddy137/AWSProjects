<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define. It's useful because it gives you complete control over your network setup—including IP address ranges, subnets, route tables, security groups, and network ACLs. With a VPC, you can design secure, scalable infrastructure that matches your application’s needs while keeping sensitive resources private and protected.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure network environment by setting up both public and private subnets. I started by launching a private subnet within my VPC to isolate sensitive resources. Then, I created a dedicated route table that only allows local traffic and associated it with the private subnet. Finally, I set up a custom network ACL to control inbound and outbound traffic more securely. Altogether, Amazon VPC helped me build a structured, secure, and customizable network for my applications.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how the default route table and network ACL are automatically associated with new subnets unless explicitly changed. It was a good reminder that AWS has convenient defaults, but if you're aiming for tighter security—especially for private subnets—you need to manually override those defaults to avoid exposing resources unintentionally.

### This project took me...

This project took me approximately 30 to 45 minutes. The setup steps were clear, but I took a bit of extra time to explore the differences between public and private subnets, understand route table behavior, and configure custom network ACLs properly. It was a great hands-on experience to reinforce VPC fundamentals!

---

## Private vs Public Subnets

The difference between public and private subnet is that the public subnet will get to communicate with the internet,whereas the private subnet can only communicate with the resources within the vpc.

Having private subnets are useful because they allow you to isolate sensitive resources—like databases, backend services, or internal applications—from the public internet. This enhances security by preventing direct exposure of critical infrastructure while still allowing these resources to communicate internally within the VPC or access the internet indirectly (e.g., through a NAT gateway). Private subnets help enforce the principle of least privilege, reducing attack surfaces and improving control over your cloud environment.

My private and public subnets cannot have the same IPv4 CIDR block because each subnet within a VPC must have a unique range of IP addresses. Overlapping CIDR blocks would cause conflicts in routing and addressing, which is why AWS throws an error if you try to assign the same CIDR block to multiple subnets.


![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with NextWork Public Route Table because it’s the default route table for the entire VPC. Until I explicitly associate the private subnet with a different route table—like NextWork Private Route Table—it inherits the default one, which includes a route to the internet gateway, making it public.

I had to set up a new route table because my private subnet should not have a route to the internet gateway. The default route table (NextWork Public Route Table) includes a route to the internet, which would make any associated subnet public. By creating a new route table without an internet route, I can ensure that my private subnet remains isolated and secure for internal-only communication.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows local traffic within the VPC. This means resources in the private subnet can communicate with other resources inside the same VPC (like EC2 instances, databases, etc.), but they cannot send or receive traffic directly from the internet.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the default network ACL that was automatically created with my VPC. This default ACL allows all inbound and outbound traffic, which is not ideal for a private subnet—so I created and associated a custom NACL (NextWork Private NACL) to enhance security.


I set up a dedicated network ACL for my private subnet because the default network ACL allows all traffic by default, which isn't secure for private resources. By creating a custom network ACL, I can define stricter inbound and outbound rules to control the type of traffic that can reach or leave my private subnet—helping to protect sensitive components like databases from unnecessary exposure.

My new network ACL has two simple rules — one inbound and one outbound rule that both allow local traffic within the VPC. These rules ensure that the private subnet can communicate internally with other VPC resources but block unnecessary or unsolicited external traffic, maintaining the security and isolation expected of a private environment.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-private_1ed2cb07)

---

---
