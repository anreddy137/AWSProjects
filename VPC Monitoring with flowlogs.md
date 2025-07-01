<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create your own isolated network environment within the AWS cloud, where you can launch resources like EC2 instances, databases, and containers securely. It’s useful because it gives you complete control over your network settings, such as IP ranges, subnets, route tables, internet gateways, security groups, and network ACLs.

With a VPC, you can design and manage a custom, secure cloud network that mirrors a traditional on-premises data center—while taking full advantage of AWS scalability, flexibility, and automation.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create two separate virtual networks (VPCs) from scratch, each with its own subnet and EC2 instance. I then set up a VPC peering connection between them to allow the EC2 instances to communicate privately using their internal IP addresses. After that, I configured route tables to ensure traffic could flow between the VPCs, and finally, I enabled VPC Flow Logs to monitor and analyze the network traffic for visibility and troubleshooting.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that even after launching EC2 instances and setting up the peering connection, the ping test using private IPs failed at first because the route tables weren't correctly configured to use the peering connection. It was a good reminder that just creating a peering connection isn’t enough—both VPCs also need explicit routes added to direct traffic through it.

### This project took me...

This project took me approximately 1.5 to 2 hours to complete. The time included setting up two VPCs, launching EC2 instances, configuring a peering connection, updating route tables, testing connectivity, setting up flow logs, creating IAM roles and policies, and analyzing logs in CloudWatch. The most time-consuming part was troubleshooting the connectivity and permissions issues, which gave me valuable hands-on experience with real-world AWS networking challenges.

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I’m going to create two new VPCs using the VPC wizard to quickly generate the essential components like subnets, route tables, and internet gateways. I’m doing this to rebuild a basic multi-VPC architecture that will allow me to not only practice VPC peering again but also set up and test VPC Flow Logs across multiple networks. This setup will give me a solid environment for monitoring and analyzing network traffic between isolated VPCs using AWS monitoring tools.

### Step 2 - Launch EC2 instances

In this step, I’m going to launch one EC2 instance into each of my two VPCs—NextWork-1 and NextWork-2. I’m doing this so the instances can later communicate with each other over the VPC peering connection, generating network traffic that I’ll be able to capture and analyze using VPC Flow Logs. These EC2 instances will help simulate real activity between the two VPCs, which is essential for testing and observing how traffic flows across my architecture.


### Step 3 - Set up Logs

In this step, I’m going to set up VPC Flow Logs, which will allow me to track all the network traffic going in and out of my VPCs. These logs will capture details like the source and destination IPs, ports, protocols, and whether the traffic was accepted or rejected. I’ll also set up a CloudWatch log group to store these records so I can review and analyze them later. This is important because it gives me visibility into what kind of traffic is flowing through my network and helps identify any unusual or unauthorized activity.

### Step 4 - Set IAM permissions for Logs

In this step, I'm going to complete the setup of my VPC Flow Log by assigning the right permissions so it can send traffic data to Amazon CloudWatch. Flow Logs need explicit permission to write log data to CloudWatch, and this is done by attaching an IAM role with the appropriate policy.

Once I assign the role, I’ll finalize the flow log settings—like the log group name (NextWorkVPCFlowLog), setting the filter to "All" (to capture both accepted and rejected traffic), and choosing an aggregation interval, typically 1 minute for detailed monitoring.

This will allow me to start tracking network activity inside my VPC, giving me visibility into what kind of traffic is moving through and how my security configurations are impacting it.

---

## Multi-VPC Architecture

I started my project by launching two new VPCs from scratch using the VPC wizard. The first one, NextWork-1, was created with the CIDR block 10.1.0.0/16, and the second one, NextWork-2, with 10.2.0.0/16 to ensure they had unique IP ranges. Each VPC was configured with 1 public subnet and no private subnets, using just 1 Availability Zone and skipping NAT gateways and VPC endpoints to keep things simple. This setup gives me a clean, cost-effective environment to test VPC peering and practice monitoring network traffic with VPC Flow Logs.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16, respectively. They have to be unique because each VPC needs its own distinct IP address range to avoid conflicts and ensure proper routing between them, especially when setting up a peering connection. If the CIDR blocks overlapped, it would be impossible for AWS to determine which VPC the traffic should be routed to, causing communication failures.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow All ICMP - IPv4 traffic from all IP addresses (0.0.0.0/0). This is because I need the instances in each VPC to respond to ping (ICMP) requests so I can test the VPC peering connection and generate network activity. Allowing ICMP from all sources ensures that traffic between the two instances won’t be blocked at the security group level, which is essential for both connectivity testing and flow log monitoring later in the project.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are detailed records of events and activities that happen within your systems or applications. They capture information such as user actions, network requests, system errors, and performance metrics. In AWS, logs help engineers monitor behavior, troubleshoot issues, and track security events. They’re essential for understanding what’s happening behind the scenes in your infrastructure and are a key tool for maintaining performance, reliability, and security.

Log groups are organized containers in Amazon CloudWatch where related logs are stored together. Each log group acts like a folder that holds logs from the same source—such as a specific VPC, EC2 instance, or application. This organization helps keep logs structured and easy to manage, making it simpler to analyze traffic patterns, detect issues, and monitor performance. Since logs are region-specific, each log group stores data only for the region where it was created.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy because VPC Flow Logs need explicit permission to create and send log data to CloudWatch. Without this policy, the flow logs wouldn’t be able to generate or store any traffic records. The policy allows actions like creating log groups and streams, sending log events, and describing existing logs. This ensures that the logs generated by my VPC's network traffic can be captured and stored securely in CloudWatch for monitoring and analysis.

I also created an IAM role because VPC Flow Logs need a role to assume in order to gain the permissions defined in the IAM policy I just created. While the policy outlines what actions are allowed—like creating log streams and sending log data to CloudWatch—the role acts as the container that holds those permissions. By assigning this role to VPC Flow Logs and using a custom trust policy, I made sure that only VPC Flow Logs can use this role, ensuring secure and controlled access to log-related actions in my AWS environment.

A custom trust policy is a specific type of policy that defines who or what is allowed to assume an IAM role. Unlike regular IAM policies that control what actions a role can perform, a custom trust policy focuses on the identity of the service or user that’s allowed to use the role. In this case, I used a custom trust policy to explicitly allow only the VPC Flow Logs service (vpc-flow-logs.amazonaws.com) to assume the role, ensuring that no other AWS service or user can use it. This adds a strong layer of security by tightly controlling access to the permissions granted by the role.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I’m going to use EC2 Instance Connect to access the instance in VPC 1 and try sending a network request to the instance in VPC 2 using its private IP address. I’m doing this to test whether the VPC peering connection between the two VPCs is working properly, and also to generate some traffic that will show up in my VPC Flow Logs. This way, I can confirm both connectivity and that my monitoring setup is capturing traffic as expected.

### Step 6 - Set up a peering connection

In this step, I'm going to create a VPC peering connection between my two VPCs—NextWork-1 and NextWork-2—to establish a private network path between them. Right now, the instances in each VPC can only communicate over the internet, which isn’t secure or efficient. By setting up this peering connection and updating the route tables in both VPCs, I’ll enable direct, private communication using their internal IP addresses, which is exactly what peering is designed for. This is the missing link that will let the instances talk to each other securely within AWS.

### Step 7 - Analyze flow logs

In this step, I’m going to review the VPC Flow Logs for VPC 1’s public subnet to see what kind of network traffic was captured. I’ll be looking for records that show the ping requests and responses between the EC2 instances in VPC 1 and VPC 2. This is important because it lets me confirm that my flow log setup is working and that I can track and analyze traffic between my VPCs. These insights help ensure that my network is behaving as expected and give me visibility into how my resources are communicating.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means Instance - NextWork VPC 1 was able to send the request, but Instance - NextWork VPC 2 either didn’t receive it or didn’t respond. This usually indicates a configuration issue, such as a missing security group rule, incorrect route table setup, or a network ACL blocking the traffic. Since I’m testing both VPC peering and flow log activity, this response shows that some part of the communication path still needs to be fixed before traffic can flow between the two instances.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means the instances can communicate over the internet, but not through their private IPs via the VPC peering connection. This suggests that while both instances are publicly accessible, the private network path between the VPCs isn’t properly configured yet—likely due to missing routes, security group rules, or network ACL settings that are preventing private traffic from flowing through the peering connection.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because there was no route directing traffic to VPC 2’s CIDR block (10.2.0.0/16) through the VPC peering connection. Without this route, Instance 1 didn’t know how to reach Instance 2 over the private network, so the traffic never made it through the peering link. Instead, the only route available for external traffic was through the internet gateway, which isn’t used for private IP communication between VPCs.

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables so that each VPC knows how to send traffic to the other using the peering connection. Without these routes, even though the peering connection exists, the VPCs wouldn’t know how to reach each other’s IP ranges privately. By adding a route in VPC 1's table for VPC 2's CIDR block (10.2.0.0/16) and vice versa, I made sure that traffic between the two VPCs flows directly over the private peering link instead of going through the public internet.


![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means the VPC peering connection is working correctly, and the route tables and security group settings are properly configured to allow private network communication between the two instances. The traffic is flowing securely over the private link between VPCs, without needing to go through the public internet—just as intended with VPC peering.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about the details of network traffic flowing to and from network interfaces in our VPC. Each log entry includes important information such as the source and destination IP addresses, ports, protocols used, traffic direction (inbound or outbound), and most importantly, whether the traffic was ACCEPTED or REJECTED based on security group and network ACL settings. These logs give engineers clear visibility into what's happening at the network level—helping with troubleshooting, security auditing, and optimizing network performance.

For example, the flow log I've captured tells us that a ping request was sent from Instance 1 to Instance 2, including details like the source IP (from VPC 1), the destination IP (in VPC 2), the protocol used (ICMP), and whether the traffic was accepted or rejected. If the log ends in ACCEPT OK, it means the traffic successfully passed through the network rules. If it says REJECT OK, it means the traffic was blocked—likely before I set up proper routes or security group rules. This gives me clear insight into how my network is behaving and where issues might be occurring.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is a powerful tool in Amazon CloudWatch that lets you run queries on your log data to analyze and extract meaningful information. Instead of manually scrolling through endless logs, you can use Logs Insights to quickly filter, search, and even perform calculations on the data—like finding patterns, detecting anomalies, or pinpointing errors. It’s especially useful when you're working with large volumes of logs and need to understand what's happening in your system efficiently.

I ran the query fields @timestamp, interfaceId, srcAddr, dstAddr, action | sort @timestamp desc | limit 20. This query analyzes the most recent 20 flow log entries by displaying the timestamp, network interface ID, source IP address, destination IP address, and whether the traffic was accepted or rejected. It helps me quickly understand the flow of traffic in my VPC and see if there were any failed or unexpected network interactions between my resources.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-monitoring_3e1e79a1)

---

---
