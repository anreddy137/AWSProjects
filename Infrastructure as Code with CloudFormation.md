<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Infrastructure as Code with CloudFormation

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-cloudformation-updated)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

## Introducing Today's Project!

In this project , i will demonstrate CICD infrastructure into a handy template with cloudformation.

### Key tools and concepts

Services i used were codebuild , codedeploy, cloudformation, s3 , ec2

### Project reflection

This project took me around 120 minutes

Project 6

---

## Generating a CloudFormation Template

the IAC generator scans the resources .

A cloudformation template is 

The resources i couldn't add to my template were

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_0495b046)

---

## Template Testing

Before testing my template , i will delete all my resources because i will be deploying it using the template that i just created.

I tested my template by creating a stack.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_f56730fd)

---

## DependsOn

To resolve the error , i added a depends on line so it only starts once whtever in the dependsOn is done.

The dependsOn line was added to four different parts of my template , for codeartifact policy

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_f0df8018)

---

## Circular Dependencies

I gave my cloudformation template another test 

To  fix this error , 

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_e6fd85ed)

---

## Manual Additions

---

## Success!

I could verify all the deployed resources by visiting the resources tab

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

---
