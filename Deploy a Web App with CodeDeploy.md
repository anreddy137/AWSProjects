<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy a Web App with CodeDeploy

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codedeploy-updated)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-27)

---

## Introducing Today's Project!

In this project, I will demonstrate how to automate the deployment of a web application using AWS CodeDeploy and CloudFormation. I'm doing this project to learn how to set up a repeatable, reliable deployment process that minimizes manual effort, reduces the risk of errors, and ensures that my application is consistently deployed across environments. I’ll also implement a rollback strategy to recover quickly from deployment failures—an essential disaster recovery technique in real-world DevOps workflows.

### Key tools and concepts

Services i used were code build , code deploy, code artifact , cloud formation, ec2, s3.

### Project reflection

This project took me more than two hours

This project is part five of a series of devops projects where ii am building a cicd pipeline ! i will ne working on the next project now.

---

## Deployment Environment

To set  up for codedeploy , i launched an EC2 instance and VPC because 

instead of launching these resources manually , i used cloudformation template to launch all the required 

Other resources created in this template include an IAM role internet gateway and an ec2 instance.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-5)

---

## Deployment Scripts

Scripts are a set of files that automates our deployment .

install_dependencies will have several files to install apache, tomcat and proxypass and proxyrequest.

start_server.sh starts the apache and tomcat .

stop_server.sh will stop the servers.

---

## appspec.yml

then, i wrote an appspec.yml file to create the instructions for the codedeploy.

i also updated buildspec.yml because 

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-12)

---

## Setting Up CodeDeploy

A deployment group is 

to set up a deployment group , you also need to create an IAM role to 

Tags are helpful for identifying the resources , i used the tag to

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-18)

---

## Deployment configurations

Another key settings is the deployment configuration , which affects ..

In order to connect , a code deploy agent is also set up 

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-20)

---

## Success!

A code deploy deployment represents a single code deployment , represents a single deployment .

i had to configure a revision location which means my revisipn was 

To check that the deployment was a succcess , i visited the deployment page .

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codedeploy-updated_val-27)

---

## Disaster Recovery

---

---
