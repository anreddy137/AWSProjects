<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create a private, isolated section of the AWS cloud where you can launch and manage resources like EC2 instances, databases, and load balancers. It’s like building your own secure data center in the cloud with full control over your networking environment—including IP address ranges, subnets, route tables, and gateways.

It’s useful because it allows you to define how your resources communicate with each other and with the internet, apply strict security rules, and ensure your infrastructure is scalable, secure, and well-organized. With Amazon VPC, you can build highly available and resilient architectures while keeping your data and applications protected.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to build a secure and structured networking environment in the cloud. I created a custom VPC, set up a public subnet within it, and attached an internet gateway to allow internet access. I also configured a route table to direct traffic to the internet gateway, created a security group to control access to individual resources, and added a network ACL for subnet-level traffic filtering. Finally, I explored EC2 Global View to track resources across multiple regions. This helped me understand how to control traffic flow, secure my infrastructure, and manage resources efficiently across different AWS regions.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how layered and interconnected the security configurations are in a VPC. Setting up a security group wasn’t enough—I also had to configure route tables, network ACLs, and ensure the internet gateway was properly attached and routed. It showed me that even small missteps, like missing a route or having conflicting rules, can block traffic completely. It was a great reminder that cloud networking requires careful planning and attention to detail.

### This project took me...

This project took me approximately 1 to 1.5 hours. A good portion of the time went into carefully creating and linking each VPC component—like the subnet, internet gateway, route table, security group, and network ACL—and then verifying everything worked as expected. Switching regions and using the AWS CLI added some extra steps, but it was a valuable experience in understanding how to manage VPC resources efficiently across different environments.


---

## Route tables

Route tables are sets of rules within a VPC that control where network traffic is directed. Each rule, called a route, tells the traffic where to go—whether it's to another subnet, out to the internet, or to a specific gateway. Every subnet in a VPC must be associated with a route table because the table acts like a GPS, guiding the flow of data to the right destination. For example, to allow internet access, a route table must include a route that sends all outbound traffic (0.0.0.0/0) to the internet gateway. Without the right routes in place, even connected resources won't know how to reach the outside world or each other.

Route tables are needed to make a subnet public because they define how traffic flows in and out of the subnet. For a subnet to be considered public, its route table must include a route that directs internet-bound traffic (typically 0.0.0.0/0) to an internet gateway. Without this route, even if the subnet is associated with an internet gateway and the instances have public IP addresses, the traffic has no path to reach the internet. The route table is what officially connects the subnet to the outside world.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which mean the destination is the IP range the traffic is trying to reach, and the target is where the traffic should be sent to get there. For example, a destination of 0.0.0.0/0 means all traffic heading to the internet, and a target of an internet gateway tells AWS to send that traffic out through the internet gateway. This pairing is what allows AWS to correctly direct network traffic based on where it’s going and how it should get there.


The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of my internet gateway ID. This setup allows all outbound traffic from my public subnet to be routed through the internet gateway, enabling internet access for resources like EC2 instances.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are virtual firewalls that control the traffic allowed in and out of individual resources in your VPC, like EC2 instances. They act like security checkpoints for each resource, defining which types of network traffic—based on IP addresses, protocols, and port numbers—are allowed to reach or leave that resource. Unlike network-level controls, security groups are applied directly to the resource, not to the whole VPC or subnet. They help protect your infrastructure by filtering traffic and ensuring only the right types of communication are permitted.

### Inbound vs Outbound rules

Inbound rules are the settings in a security group that control what kind of incoming traffic is allowed to reach a resource, such as an EC2 instance. These rules define the source IP, the protocol, and the port number that are permitted to access the resource.

I configured an inbound rule that allows HTTP traffic on port 80 from 0.0.0.0/0, which means any device on the internet can send web requests to my resource—necessary for making a public-facing website accessible to all users.

Outbound rules are the settings in a security group that control what kind of outgoing traffic is allowed to leave a resource and reach other destinations, such as the internet or other services. These rules specify the destination IP, the protocol, and the port number that are permitted for outgoing connections.

By default, my security group's outbound rule allows all traffic to go out to any destination (0.0.0.0/0), using all protocols and port ranges. This means that the resources in my VPC can initiate connections to the internet or other services without restriction.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are virtual firewalls that operate at the subnet level in a VPC, controlling the flow of data packets into and out of subnets. They act like traffic cops, inspecting each packet based on a numbered list of rules to decide whether to allow or deny the traffic. Unlike security groups, which are attached to individual resources, network ACLs apply to entire subnets and affect all resources within them. They support both allow and deny rules and evaluate traffic in order from the lowest rule number to the highest, offering broad and customizable control over subnet-level traffic behavior.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that a security group acts as a virtual firewall at the resource level, controlling traffic to and from specific instances, while a network ACL operates at the subnet level, managing traffic entering and leaving the entire subnet. Security groups are stateful, meaning if traffic is allowed in, the response traffic is automatically allowed out. In contrast, network ACLs are stateless, so return traffic must be explicitly allowed by separate outbound rules. Security groups are used for fine-grained access control to individual resources, whereas network ACLs provide broader, subnet-wide traffic filtering.

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic. This means every type of traffic—regardless of protocol, port number, or IP address—is permitted to flow in and out of the subnet unless you explicitly modify the rules to deny or restrict it. This default setting provides open access but should be customized to enhance security.


In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all traffic. This means no traffic is allowed into or out of the subnet until you explicitly add rules to permit it. You have to manually create allow rules for the specific types of traffic you want, such as allowing HTTP or SSH, giving you full control over what is permitted.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

I created additional VPC resources using the AWS CLI: a VPC, an internet gateway, and a security group. Instead of my usual region, I used a different region code to deploy these resources in a new location. Teams would use multiple regions to ensure high availability, minimize latency for users in different parts of the world, and strengthen disaster recovery strategies by distributing infrastructure across geographically isolated regions.

EC2 Global View is a tool where you can find all your EC2-related resources—like instances, VPCs, subnets, security groups, and internet gateways—across every AWS region in your account. I could even narrow down my search by filtering resources by type or region, which made it easy to track what I’ve deployed and where. Without EC2 Global View, you’d have to manually switch between regions in the AWS Console to view your resources one by one, which is time-consuming and easy to miss things.

Now that I've learnt about EC2 Global View, I'd use it again to quickly check and manage all my EC2 and VPC resources across every AWS region from one place. It’s especially useful when working on global projects, cleaning up unused resources, auditing deployments, or ensuring consistency across environments without needing to manually switch between regions in the console.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-security_b03ea6162)

---

---
