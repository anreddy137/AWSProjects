<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC, or Virtual Private Cloud, is a service that allows you to create your own isolated network environment within the AWS cloud. It's like setting up a private data center in the cloud where you can control everything—from how your resources connect to each other, to what traffic is allowed in and out. This makes it incredibly useful for keeping your applications secure, managing internal communication between services, and connecting safely to the internet or other AWS services. It essentially gives you full control over your network architecture while still benefiting from the scalability and flexibility of the cloud.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create a secure, isolated environment for launching my EC2 instance. I set up a public subnet within the VPC, allowing the instance to access the internet. This VPC setup enabled my EC2 instance to interact with Amazon S3 through the AWS CLI after configuring access credentials. By using the VPC, I ensured that my resources were organized, securely managed, and could communicate effectively within a controlled network space.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easily the EC2 instance could access and interact with Amazon S3 once the access keys were properly configured. I initially thought it would require more setup or permissions, but once the credentials were in place, the CLI commands worked smoothly. It was a great reminder of how powerful and seamless AWS integrations can be when configured correctly.

### This project took me...

This project took me approximately 1.5 to 2 hours to complete. Most of the time was spent carefully setting up the VPC and EC2 instance, configuring access credentials securely, and making sure the S3 bucket interactions via the CLI were working correctly. It was a hands-on and insightful experience overall.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I’m creating the foundational infrastructure for the project by setting up a new VPC and launching an EC2 instance inside it. This VPC will act as the isolated network environment for my resources, and the EC2 instance will serve as the compute resource that I’ll use to interact with Amazon S3 later in the project. Setting these up is essential because they provide the secure and controlled environment from which I’ll access other AWS services.

### Step 2 - Connect to my EC2 instance

In this step, I'm connecting directly to my EC2 instance using EC2 Instance Connect. This gives me access to the instance’s terminal, where I can run commands and interact with other AWS services like S3. This direct access is essential for testing whether my EC2 instance can communicate with services outside the VPC, which is a key goal of this project.

### Step 3 - Set up access keys

In this step, I'm going to create access keys so that my EC2 instance can securely interact with AWS services like Amazon S3. Without these credentials, the instance doesn’t have permission to perform actions on my behalf. By creating and configuring access keys, I’m giving my instance the necessary authentication to use AWS CLI commands and access my AWS environment.

---

## Architecture set up

I started my project by launching a new VPC named NextWork with a CIDR block of 10.0.0.0/16, including 1 public subnet and no private subnets. Then, I launched an EC2 instance into this VPC using the Amazon Linux 2023 AMI, t2.micro instance type, and enabled the Auto-assign public IP option to make sure the instance can connect to the internet. This setup lays the foundation for accessing Amazon S3 from within my VPC.

I also set up an S3 bucket named nextwork-vpc-project-[myname] to store files that my EC2 instance can access. After creating the bucket, I uploaded two files from my local computer into it. This allows me to test how my EC2 instance can interact with S3 using AWS CLI commands.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a command-line tool that lets me interact with AWS services directly from a terminal using simple commands. I have access to AWS CLI because it's pre-installed on EC2 instances by default, which means I can run commands like aws s3 ls to manage and explore AWS services such as S3 right from within my instance.

The first command I ran was aws s3 ls... This command is used to list all the Amazon S3 buckets that my AWS credentials have permission to access. It helps verify whether my EC2 instance is successfully authenticated to interact with the S3 service.

The second command I ran was aws configure... This command is used to set up AWS credentials (like the access key ID and secret access key), default region, and output format for the AWS CLI on my EC2 instance. It ensures that the instance can securely access and interact with AWS services like S3.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured it using the aws configure command. This command allowed me to enter my access key ID, secret access key, default region, and output format. With this configuration, my EC2 instance can now securely use the AWS CLI to interact with services like Amazon S3 from within the terminal.

Access keys are a set of security credentials that allow programmatic access to your AWS account. They consist of two parts: an Access Key ID and a Secret Access Key. These credentials are used by applications or services, such as an EC2 instance running the AWS CLI, to authenticate and interact with AWS services like S3, without needing to log in through the AWS Management Console.

Secret access keys are the private part of your AWS credentials that, when combined with your access key ID, allow you to securely access and interact with AWS services. They function like a password, and must be kept confidential—if someone else gets access to your secret key, they could potentially control your AWS account.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM roles. IAM roles allow you to grant temporary permissions to your EC2 instance without hardcoding credentials. This approach is more secure because there are no access keys to accidentally expose or rotate manually, and AWS handles the credential management automatically behind the scenes.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I'm going to create a new S3 bucket so I can store files in it and later access those files from my EC2 instance. This is important because it helps me understand how services inside my VPC can interact with other AWS services like S3, which is a common use case in real-world cloud applications.

### Step 5 - Connecting to my S3 bucket

In this step, I'm going to use my EC2 instance to connect to the S3 bucket I created earlier. The goal is to make sure that my instance can successfully access and interact with other AWS services—in this case, S3. This will confirm that the access keys I set up are working correctly and that my instance has the right permissions to list and manage files in the bucket.

---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls... This command is used to list all the Amazon S3 buckets that my AWS credentials have permission to access. It helps verify whether my EC2 instance is successfully authenticated to interact with the S3 service.

When I ran the command aws s3 ls again, the terminal responded with a list of my S3 buckets, including the one I just created. This indicated that my EC2 instance was successfully authenticated and now has permission to access my AWS environment and interact with S3.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls  which returned a list of the two files I had uploaded to my S3 bucket earlier. This confirmed that my EC2 instance could not only access S3, but also view the contents of a specific bucket using the AWS CLI.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/test.txt. This command creates a blank text file named test.txt in the /tmp directory of my EC2 instance, which I then used to practice uploading to my S3 bucket.

The second command I ran was aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-nit. This command will copy the test.txt file from my EC2 instance's /tmp directory and upload it to my S3 bucket, allowing me to store files from my instance directly into S3.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-yourname... which validated that my new file test.txt had been successfully uploaded to the bucket. I could now see three objects listed: the two original files I uploaded earlier and the new test.txt file created from my EC2 instance.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-s3_3e1e79a2)

---

---
