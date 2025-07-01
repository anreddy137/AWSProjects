<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create your own isolated network environment within AWS. It’s like building your own private data center in the cloud, where you can launch AWS resources like EC2 instances, control their networking, and set up security rules.

It’s useful because it gives you full control over how your resources connect to each other, to the internet, and to other AWS services—helping you design secure and scalable applications in the cloud.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create a secure and isolated network for my resources. I launched an EC2 instance inside this VPC, created a public subnet to allow connectivity, and set up a VPC endpoint to connect directly to an S3 bucket without using the public internet. This setup helped ensure secure communication between my instance and the S3 bucket, demonstrating how VPCs can be configured for both functionality and tighter security.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that even after successfully accessing my S3 bucket from the EC2 instance using access keys, the connection was still going through the public internet. I assumed that resources inside the same AWS environment would communicate privately by default, but learning that a VPC endpoint was needed to establish a secure, private connection was surprising and really emphasized the importance of managing network traffic securely.

### This project took me...

This project took me approximately 1 hour and 20 minutes to complete. The most time-consuming parts were setting up the bucket policy and troubleshooting endpoint access, but they were also the most insightful. It was rewarding to see the secure communication between my EC2 instance and S3 bucket finally work as intended.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I'm setting up the core components of my architecture: a VPC, an EC2 instance, and an S3 bucket. I need the VPC to create a secure and isolated network environment, the EC2 instance to simulate a compute resource inside the VPC, and the S3 bucket to store files I’ll access later. This setup is the foundation for testing how to connect from the EC2 instance to the S3 bucket securely using a VPC endpoint.

### Step 2 - Connect to EC2 instance

In this step, I'm connecting directly to my EC2 instance using EC2 Instance Connect so I can test how it interacts with my S3 bucket without a VPC endpoint in place. This will help me understand the default behavior—how the EC2 instance accesses S3 over the public internet—and set a baseline for comparison once the VPC endpoint is added.

### Step 3 - Set up access keys

In this step, I’m setting up access keys so that my EC2 instance can securely interact with my AWS services like S3. Since the EC2 instance needs credentials to run AWS CLI commands and access resources in my account, I’m creating an access key ID and a secret access key through IAM. This will let my instance authenticate itself and perform actions like listing buckets or uploading files without needing to go through the console.

### Step 4 - Interact with S3 bucket

In this step, I'm heading back to my EC2 instance to test whether it can access my S3 bucket now that I've configured access keys. This will confirm that the credentials are working and that my instance can communicate with S3 services directly from within the VPC.

---

## Architecture set up

I started my project by launching a new VPC named NextWork, along with a public subnet, and then deployed an EC2 instance named Instance - NextWork VPC Endpoints into that VPC. I also created a new security group called SG - NextWork VPC Endpoints for the instance. This setup gives me a basic network and compute environment to test secure access to S3 using VPC endpoints.

I also set up an S3 bucket named nextwork-vpc-endpoints-nithyasri in the same Region as my VPC. After creating the bucket, I uploaded two files from my local computer to it. This prepares the bucket for access testing from my EC2 instance using a VPC endpoint, without going through the public internet.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured four things: the Access Key ID, the Secret Access Key, the Default region name, and left the Default output format blank. This setup allows the instance to authenticate and use the AWS CLI to access services like S3 securely.

Access keys are a set of security credentials used to authenticate and authorize access to AWS services from outside the AWS Management Console, like from an EC2 instance or a local machine. They consist of two parts: an access key ID (which acts like a username) and a secret access key (which acts like a password). Together, they allow your applications or resources to securely interact with AWS APIs and services like S3, EC2, and more.

Secret access keys are the private part of your AWS credentials, used alongside your access key ID to authenticate requests made to AWS services. You can think of them as the password that goes with your username (the access key ID). Since they provide full access to your AWS account when paired, they must be kept secure and never shared or exposed—if someone else gets access to your secret key, they could control your AWS resources.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM roles with specific permissions attached. IAM roles allow your EC2 instance to securely access AWS services without needing to store access keys directly on the instance. This greatly reduces the risk of accidental exposure or misuse of credentials, and it simplifies credential management by letting AWS handle the temporary credentials automatically.

---

## Connecting to my S3 bucket

The command I ran was aws s3 ls... This command is used to list all the S3 buckets in my AWS account that my current credentials have permission to access. It’s a quick way to verify if my EC2 instance can successfully communicate with the S3 service using the AWS CLI.



The terminal responded with a list of my S3 buckets, including vpc-endpoints-yourname. This indicated that the access keys I set up are working correctly and my EC2 instance now has permission to access my AWS environment and interact with S3.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

I also tested the command aws s3 ls s3://nextwork-vpc-endpoints-yourname, which returned a list of the files I had uploaded to the bucket. This confirmed that my EC2 instance could successfully connect to the S3 bucket and read its contents over the internet.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/test.txt. This command creates a blank text file named test.txt in the /tmp directory of my EC2 instance, which I could then upload to my S3 bucket.


The second command I ran was aws s3 cp /tmp/test.txt s3://nextwork-vpc-endpoints-yourname. This command will copy the test.txt file from the EC2 instance’s /tmp directory to my S3 bucket, effectively uploading the file to the cloud.

The third command I ran was aws s3 ls s3://nextwork-vpc-endpoints-yourname, which validated that the new file test.txt was successfully uploaded to my S3 bucket by listing it alongside the previously uploaded files.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I'm setting up a VPC endpoint to allow my EC2 instance to communicate directly with my S3 bucket without using the public internet. This adds a layer of security by keeping all traffic within the AWS network, reducing exposure to external threats and making the communication between services more private and secure.

### Step 6 - Bucket policies

In this step, I'm going to secure my S3 bucket by writing a bucket policy that blocks all access except for requests coming specifically through my VPC endpoint. This will help confirm that the VPC endpoint is set up correctly and that my EC2 instance is communicating with S3 over a private, secure connection instead of the public internet.

### Step 7 - Update route tables

In this step, I’m going to test whether my EC2 instance can still access the S3 bucket now that the bucket policy only allows traffic from my VPC endpoint. This will help me confirm that the VPC endpoint has been set up correctly and is enabling secure, private communication between my EC2 instance and the S3 bucket—without going through the public internet.

### Step 8 - Validate endpoint conection

In this step, I'm about to test whether my EC2 instance can still access my S3 bucket now that all the secure configurations—including the VPC endpoint and bucket policy—are in place. This will confirm that my instance is communicating with S3 through a private, secure path without relying on the public internet. If the connection works, it means my VPC endpoint setup is successfully protecting traffic while still allowing access.

---

## Setting up a Gateway

I set up an S3 Gateway, which is a type of VPC endpoint that allows my VPC to privately connect to Amazon S3 without using the public internet. Instead of routing traffic through the internet, it updates the VPC's route table so that all S3-related requests go through this gateway, keeping the communication secure and within the AWS network.

### What are endpoints?

An endpoint is a private connection that allows resources inside a VPC to communicate directly with supported AWS services like S3, without sending traffic over the public internet. It helps improve security by keeping data within the AWS network, reducing exposure to external threats.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a set of permissions written in JSON that you attach directly to an S3 bucket to control who can access the bucket and what actions they can perform. It lets you define very specific access rules—such as allowing or denying access based on the source IP, AWS account, or in this case, a VPC endpoint. This helps ensure that only trusted traffic is allowed to interact with your bucket.

My bucket policy will restrict access so that only traffic coming through my specific VPC endpoint can interact with the S3 bucket. This means even if someone has the right access keys, they won't be able to access the bucket unless their request is routed through the trusted endpoint. It's a strong way to enforce private, secure communication between my EC2 instance and the S3 bucket.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because the new policy blocked all access to the bucket except requests coming specifically from my VPC endpoint. Since the S3 console in the browser doesn't use the VPC endpoint and instead accesses S3 over the public internet, it got blocked by the policy—exactly as intended.

I also had to update my route table because the S3 Gateway endpoint needs a specific route to ensure that traffic destined for S3 is directed through the private VPC endpoint instead of the public internet. Without updating the route table, my EC2 instance wouldn't know to use the new secure path to access S3.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

To update my route table, I selected the route table associated with my public subnet in the VPC console, went to the “Routes” tab, and clicked “Edit routes.” Then I added a new route where the destination was pl-68a54001 (the prefix list ID for S3), and the target was my VPC endpoint ID. After saving the changes, my VPC could now privately route S3 traffic through the endpoint instead of the internet.

After updating my public subnet's route table, my terminal could return the list of objects in my S3 bucket. This confirmed that my EC2 instance was successfully accessing the bucket through the VPC endpoint, and not the public internet—proving that my secure, private connection setup was working exactly as intended.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a set of permissions attached to a VPC endpoint that controls which AWS services and resources the endpoint can access. It acts like a security gatekeeper, letting you define what kind of traffic is allowed or denied through that private connection. In this case, the endpoint policy restricted access to the S3 bucket, demonstrating how powerful and granular these controls can be.

I updated my endpoint's policy by changing the "Effect": "Allow" statement to "Effect": "Deny" in the policy editor. I could see the effect of this right away, because when I tried to access my S3 bucket from the EC2 instance using the aws s3 ls command, the request was denied—confirming that the endpoint policy successfully blocked access to the bucket.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-endpoints_3e1e79a3)

---

---
