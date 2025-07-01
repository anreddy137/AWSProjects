<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a logically isolated network environment in the AWS cloud, where you can launch and manage resources like EC2 instances, databases, and containers securely. It gives you full control over your networking setup, including IP address ranges, subnets (public and private), route tables, internet gateways, NAT gateways, security groups, and network ACLs.

It’s useful because it allows you to design a custom and secure network architecture, keep sensitive resources private, connect multiple environments through peering, and scale infrastructure with flexibility—just like you would in a traditional data center, but with the agility of the cloud.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to build two separate virtual networks (VPCs), configure them with public subnets, and connect them using a VPC peering connection. I launched EC2 instances into each VPC and set up the necessary route tables, security groups, and network ACLs to enable secure communication between them. I also used tools like ping to test connectivity across the peering link, and configured Elastic IPs to enable access via EC2 Instance Connect. This project helped me understand how to manage isolated networks and enable private communication between them using VPC features.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easily a missing security group rule or misconfigured network ACL could block traffic between VPCs—even when the peering connection and routes were correctly set up. It was a great reminder that VPC connectivity depends on multiple layers of configuration, and getting all of them right is essential for successful communication between instances.

### This project took me...

This project took me approximately 45 to 60 minutes. Most of the time was spent carefully setting up the two VPCs, launching EC2 instances, configuring peering, and troubleshooting connectivity issues like missing security group rules and Elastic IPs. It was a great hands-on experience that really helped reinforce how all the pieces of VPC networking work together.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I'm about to create two brand new VPCs using the VPC wizard and visual resource map. This tool makes it much faster and easier to set up the core components of a VPC—like subnets, route tables, and gateways—all in one place. Instead of manually creating each piece, I’ll use the “VPC and more” option to build out two complete VPC environments quickly and efficiently.

### Step 2 - Create a Peering Connection

In this step, I'm about to create a VPC peering connection, which is a way to directly connect two separate VPCs so they can communicate with each other using private IP addresses. This connection allows resources in one VPC (like EC2 instances) to talk to resources in another VPC as if they were in the same network, without using the internet or VPNs. It's a secure and efficient way to bridge isolated environments within AWS.

### Step 3 - Update Route Tables

In this step, I'm about to update the route tables in both VPCs to enable traffic to flow through the peering connection. Even though the peering connection is established, the VPCs won’t know how to send traffic to each other unless I manually add routes. I’ll add a route in VPC 1's route table that points to VPC 2’s CIDR block using the peering connection as the target—and then do the same in reverse for VPC 2. This tells each VPC how to reach the other.

### Step 4 - Launch EC2 Instances

In this step, I'm about to launch one EC2 instance into each of my two VPCs—NextWork-1 and NextWork-2. These instances will act as test machines to help verify that the peering connection is working correctly. Once they’re up and running, I’ll try to communicate between them using their private IPs to confirm that the routing and peering setup is successful.

---

## Multi-VPC Architecture

I started my project by launching two separate VPCs using the “VPC and more” setup wizard. The first VPC, NextWork-1, used the IPv4 CIDR block 10.1.0.0/16, and the second VPC, NextWork-2, used 10.2.0.0/16 to ensure there were no conflicts. Each VPC was created with 1 public subnet and 0 private subnets, resulting in a total of 2 public subnets across both VPCs. The setup was quick and efficient thanks to the visual resource map.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16, respectively. They have to be unique because each VPC needs a distinct range of IP addresses to avoid conflicts and ensure proper routing within and between VPCs. If two VPCs had overlapping CIDR blocks, it would create ambiguity when trying to route traffic between them, especially in scenarios involving VPC peering or shared services. Unique CIDR blocks maintain clear network boundaries and ensure reliable communication.


### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as I don't need to directly connect to them via SSH for this project. My main goal is to test network connectivity between the two instances using their private IP addresses through the VPC peering connection. Since I'm not planning to log in and manage the instances manually, skipping the key pair setup keeps things simpler.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking link between two Amazon VPCs that allows them to route traffic to each other privately using their internal IP addresses. It enables resources like EC2 instances in one VPC to communicate with resources in another VPC as if they were part of the same network. VPC peering is secure, low-latency, and does not require internet access, VPNs, or NAT gateways, making it a simple and cost-effective way to connect VPCs within or across AWS accounts and regions.

VPCs would use peering connections to securely share resources or enable communication between services hosted in different VPCs. This is useful for scenarios like connecting a backend service in one VPC to a frontend application in another, or when teams manage separate VPCs but need their systems to interact. Peering allows this communication without going over the public internet, reducing latency and improving security.

The difference between a Requester and an Accepter in a peering connection is that the Requester is the VPC that initiates the peering connection, while the Accepter is the VPC that receives and approves the request. Both sides must agree for the connection to become active. This two-step process ensures mutual consent and allows for cross-account or cross-region connectivity with proper authorization.


![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because the peering connection itself doesn’t automatically tell the VPCs how to reach each other. By adding a new route in each route table that points to the other VPC’s CIDR block through the peering connection, I ensure that traffic knows where to go. Without these routes, even though the VPCs are connected, they wouldn’t be able to communicate because there’d be no defined path for the traffic to follow.

My VPCs' new routes have a destination of 10.2.0.0/16 in VPC 1’s route table and 10.1.0.0/16 in VPC 2’s route table. The routes' target was the peering connection between VPC 1 and VPC 2, which allows traffic to flow privately between the two networks.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I'm going to connect to the EC2 instance I launched in NextWork VPC 1 using EC2 Instance Connect. This will let me access the instance's terminal directly from the AWS console. Once connected, I’ll use it to try and communicate with the instance in VPC 2 to test if the peering connection is working properly. If there’s a connection issue, I’ll troubleshoot and fix it by reviewing the instance’s security group or route settings.

### Step 6 - Connect to EC2 Instance 1

In this step, I'm going to try connecting again to my EC2 instance in NextWork VPC 1 using EC2 Instance Connect, now that I've assigned it an Elastic IP address. This should make the instance reachable from the internet. If I run into another error, I’ll troubleshoot it by checking the instance's security group, subnet settings, or any network configurations that might be blocking the connection.

### Step 7 - Test VPC Peering

In this step, I'm going to use Instance 1 in NextWork VPC 1 to test the VPC peering connection by trying to communicate with Instance 2 in NextWork VPC 2. I’ll send network messages (like a ping) from Instance 1 to Instance 2 using its private IP address. If there are any connectivity issues, I’ll troubleshoot by checking the route tables, network ACLs, and security groups to make sure all the right permissions are in place for the instances to talk to each other.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to securely access my EC2 instance in NextWork VPC 1 directly from the AWS Management Console. Since the instance doesn’t have a public IPv4 address by default, I assigned it an Elastic IP to make it reachable from the internet. EC2 Instance Connect simplifies the SSH process by handling the key pair setup for me temporarily, allowing me to run commands and test connectivity—like pinging the instance in VPC 2 to verify that my VPC peering connection is working properly.

I was stopped from using EC2 Instance Connect as my EC2 instance didn’t have a public IPv4 address assigned, which is required for the connection to work. Without a public IP or an Elastic IP, the instance isn't reachable from the internet—even through the AWS console—so I couldn’t initiate the connection until I assigned one.


![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static public IPv4 addresses that are allocated to my AWS account and can be associated with EC2 instances. Unlike the default dynamic IPs that change when an instance is stopped and restarted, Elastic IPs remain constant, making it easier to connect to instances consistently. By assigning an Elastic IP to my instance, I made it publicly reachable, which allowed EC2 Instance Connect to work properly.

Associating an Elastic IP address resolved the error because it gave my EC2 instance a stable public IPv4 address, making it reachable from the internet. EC2 Instance Connect requires a public IP to establish a secure SSH connection through the browser, and without one, the instance is effectively invisible to external access. By attaching the Elastic IP, I enabled the connection and was able to access the instance successfully.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping [Private IPv4 address of Instance - NextWork VPC 2] from the terminal of Instance 1 using EC2 Instance Connect. This command sent network packets from VPC 1's instance to VPC 2's instance, allowing me to check whether the two instances could communicate privately through the peering connection.

A successful ping test would validate my VPC peering connection because it confirms that traffic can flow between the two instances using their private IP addresses across the peering link. If Instance 1 in VPC 1 receives responses from Instance 2 in VPC 2, it means the route tables are correctly configured, the peering connection is active, and the security groups and network ACLs are allowing the necessary ICMP traffic between the two VPCs.

I had to update my second EC2 instance's security group because it wasn’t allowing inbound ICMP traffic, which is needed for ping requests from the first instance. I added a new rule that allows ICMP (All ICMP - IPv4) traffic from the security group associated with Instance 1, ensuring that only traffic from the trusted instance in VPC 1 could reach Instance 2 in VPC 2. This allowed the ping test to succeed and confirmed that the VPC peering connection was working correctly.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-peering_7a29d352)

---

---
