<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated network environment within the AWS Cloud. It allows you to define your own IP address ranges, create subnets (both public and private), configure route tables, attach internet gateways or NAT gateways, and control traffic flow using security groups and network ACLs.

It’s useful because it gives you full control over your cloud networking, improves security by isolating resources, and enables you to build scalable, highly available, and secure infrastructure—similar to a traditional on-premises data center, but with the flexibility and power of the cloud.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to test and validate the connectivity of resources within my custom virtual network. I connected to my public EC2 instance using EC2 Instance Connect, verified communication between the public and private servers using ping, and confirmed internet access from the public server using curl.

Throughout the project, I worked with various VPC components like subnets, route tables, security groups, and network ACLs to identify and resolve connectivity issues—ensuring that each resource had the correct permissions and routing paths. This helped solidify my understanding of how VPC configurations affect network communication and internet access.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how specific and critical the Network ACL and security group settings are for allowing even basic communication like ping (ICMP traffic). I initially assumed that route tables alone would handle connectivity, but I quickly realized that without the right permissions at both the subnet and instance levels, traffic—even inside the same VPC—gets blocked. It was a great reminder of how layered and precise AWS security controls really are.

### This project took me...

This project took me approximately 30 to 45 minutes. Most of the time was spent testing connectivity between instances, identifying and fixing configuration issues in the network ACLs and security groups, and understanding how tools like ping and curl validate VPC connectivity and internet access. It was a hands-on, insightful experience that reinforced key VPC concepts.

---

## Connecting to an EC2 Instance

Connectivity means the ability of different systems, devices, or networks to successfully communicate and exchange data with each other. In the context of AWS and EC2 instances, it refers to whether an instance can be accessed (e.g., via SSH), whether it can reach other instances within the same VPC, or whether it has access to external networks like the internet. Testing connectivity helps ensure that your configurations—like route tables, security groups, and subnets—are correctly set up for communication.

My first connectivity test was whether I could connect to NextWork Public Server, the EC2 instance launched in my public subnet. This test confirmed that the instance was reachable from the AWS Management Console using EC2 Instance Connect, verifying that my subnet, route table, internet gateway, and security group were all set up correctly for internet access.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a browser-based tool provided by AWS that lets you securely access your EC2 instances without needing to manage SSH keys manually. It simplifies the connection process by automatically generating a temporary SSH key pair and injecting the public key into your instance, allowing you to connect directly from the AWS Management Console. This makes it easy and fast to access instances, especially for troubleshooting or quick configuration tasks.

My first attempt at getting direct access to my public server resulted in an error, because the security group associated with the instance didn’t allow inbound SSH traffic. It only permitted HTTP traffic, which isn’t used by EC2 Instance Connect. Since EC2 Instance Connect relies on SSH to establish the connection, the missing SSH rule blocked the access attempt. Once I added an inbound rule for SSH with source set to Anywhere-IPv4, the connection was successful.

I fixed this error by editing the inbound rules of the NextWork Public Security Group and adding a new rule that allows SSH traffic (Type: SSH) from Anywhere-IPv4. This change enabled EC2 Instance Connect to establish a secure SSH connection to my public server, allowing me to access the instance directly from the AWS Management Console.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a network utility used to test whether one device can successfully communicate with another over a network. It sends a small data packet to the target device and waits for a response to measure connectivity and response time.

I used ping to test the connectivity between NextWork Public Server and NextWork Private Server, to verify whether they could communicate inside the same VPC and confirm that my networking configurations (like route tables, NACLs, and security groups) were working correctly.

The ping command I ran was ping [Private IPv4 address of NextWork Private Server], which sent ICMP packets from the NextWork Public Server to the Private Server. This command helped me check if the two instances could communicate within the VPC. When I initially saw no replies, it indicated a connectivity issue—later resolved by updating the private subnet’s Network ACL and security group to allow ICMP traffic.

The first ping returned a single line with no replies, indicating that the ping message was sent but no response came back. This meant the NextWork Public Server could attempt communication, but the traffic was blocked—most likely by the private subnet’s Network ACL or security group not allowing ICMP traffic. Once those rules were updated to permit ICMP, full ping responses started appearing.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by checking the Network ACL and security group settings for the NextWork Private Subnet and Private Server. I discovered that the Network ACL was denying all inbound and outbound traffic, including ICMP, and the security group didn’t allow ICMP either. I fixed this by adding new rules to both the Network ACL (to allow All ICMP - IPv4 from the public subnet) and the security group (to allow ICMP from the public server’s security group), which restored successful connectivity between the two servers.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a command-line tool used to send and receive data over various network protocols, most commonly HTTP and HTTPS. It allows you to test whether your machine (like an EC2 instance) can connect to a website or server on the internet. In this project, I used curl to verify that my NextWork Public Server could successfully access the internet by retrieving the raw HTML content from websites like example.com and nextwork.org.

I used curl to test the connectivity between my NextWork Public Server and external websites on the internet, like example.com and nextwork.org. By retrieving raw HTML data from those sites, I confirmed that my public subnet, internet gateway, and security settings were correctly configured to allow outbound internet access.

### Ping vs Curl

Ping and curl are different because ping checks basic network connectivity by sending ICMP packets to see if another device is reachable, while curl goes a step further by making HTTP or HTTPS requests to retrieve actual data from a web server. Ping is useful for checking if a host is online, whereas curl confirms not only connectivity but also whether higher-level internet services (like web servers) are accessible and responding properly.

---

## Connectivity to the Internet

I ran the curl command curl example.com, which returned the raw HTML content of the Example website. This confirmed that my NextWork Public Server was able to successfully reach and communicate with the internet.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-connectivity_8ee57662)

---

---
