<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App Across Accounts

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-ecr)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_3e91948719)

---

## Introducing Today's Project!

In this special multiplayer project, I'm working with a buddy to Build a Docker container image for my custom application, packaging everything it needs to run.Push and store that image securely in Amazon Elastic Container Registry (ECR), so it's ready for deployment anytime.Pull and run each other’s container images, giving us the ability to launch and explore our buddy's app as if it were our own.We're here to learn the full workflow of containerization, image sharing, and cloud-based deployment—together!

### What is Amazon ECR?

Amazon ECR (Elastic Container Registry) is a fully managed container image registry that allows you to store, manage, and deploy Docker container images in the AWS cloud. In today’s project, I used Amazon ECR to host container images built from Dockerfiles. I pushed my own image to my ECR repository and pulled my project buddy’s image from theirs. This allowed us to share applications in a containerized format and deploy them using AWS Elastic Beanstalk, making our apps live and accessible from the web. ECR acted as the central storage and distribution point for our container images throughout the project.

### One thing I didn't expect...

One thing I didn’t expect in this project was how important permission settings would be when working with Amazon ECR and Elastic Beanstalk. I assumed once the image was pushed to ECR, it would be easy to deploy—but I ran into access errors because Elastic Beanstalk and EC2 didn’t have the right roles. It taught me that managing IAM roles and repository policies is just as crucial as building and pushing the container itself.

### This project took me...

This project took me approximately 2 to 3 hours to complete. Most of the time was spent configuring permissions correctly between ECR and Elastic Beanstalk, setting up roles, and troubleshooting access issues. The Docker image build and push steps were pretty smooth, but making sure everything was wired up securely and correctly between services added a bit of extra time. Overall, it was a great hands-on experience with real-world AWS deployment challenges!

---

## Creating a Docker Image

I set up a Dockerfile and an index.html file in my local environment. Both files are needed because the Dockerfile contains the instructions for building a container image using Nginx as a base, and it tells Docker to include the custom index.html file as the web content. The index.html file is the actual web page that will be served when someone runs the container, making it essential for customizing what the user sees when they access the app.

My Dockerfile tells Docker to use the official Nginx image as the base and replace the default web page with my custom index.html file, so that my personalized content is served when the container runs.

### I also set up an ECR repository

ECR stands for Elastic Container Registry. It is important because it provides a secure, scalable, and fully managed way to store, manage, and deploy container images. By using ECR, teams can avoid the chaos of manually sharing images, ensure consistent version control, integrate seamlessly with CI/CD pipelines, and restrict access through AWS IAM for enhanced security. This helps streamline development workflows and reduces the risk of using outdated or incorrect container images.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_e7f8g9h0)

---

## Set Up AWS CLI Access

### AWS CLI can let me run ECR commands

AWS CLI is the Command Line Interface tool that lets me interact with AWS services directly from my terminal using text commands. The CLI asked for my credentials because it needs to authenticate who I am in order to securely connect to my AWS account. By providing my Access Key ID and Secret Access Key, I'm proving my identity so I can push container images to Amazon ECR and perform other AWS operations from my local machine.

To enable CLI access, I set up a new IAM user with the permission to interact with specific AWS services like Amazon ECR. I also set up an access key for this user, which means I now have an Access Key ID and Secret Access Key that let me securely authenticate and run AWS commands from my terminal. This setup allows me to use the AWS CLI without logging in through the web console, and by limiting the user's permissions, I’m following best practices to keep access secure and restricted to only what’s needed.

To pass my credentials to the AWS CLI, I ran the command aws configure. I had to provide my Access Key ID, Secret Access Key (both copied from the downloaded .csv file), the AWS Region where my ECR repository is located (e.g., us-west-2), and then pressed Enter to accept the default output format (JSON). This setup allows the CLI to authenticate my identity and connect to the correct AWS region for managing my container images.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_4aa3e4fe6)

---

## Pushing My Image to ECR

Push commands are a set of instructions provided by Amazon ECR that allow you to upload (or "push") your locally built Docker image to a specific ECR repository in your AWS account. These commands typically include authenticating Docker with ECR, tagging your Docker image with the repository URI, and then using docker push to upload the image to the cloud. They are essential for moving your container image from your local machine into a cloud environment where it can be deployed and used.

### There are three main push commands

To authenticate Docker with my ECR repo, I used the command:aws ecr get-login-password --region YOUR-REGION | docker login --username AWS --password-stdin YOUR-ACCOUNT-ID.dkr.ecr.YOUR-REGION.amazonaws.com
This command retrieves a temporary login password from AWS and uses it to log Docker into my private ECR registry so I can push images securely.

To push my container image , i ran the command docker push YOUR-ACCOUNT-ID.dkr.ecr.YOUR-REGION.amazonaws.com/YOUR-REPO-NAME:latest
Pushing means I'm uploading my locally built Docker image to my Amazon ECR repository so it can be stored in the cloud. This makes the image accessible for deployments, allowing others (like my project buddy) to pull and run the container from the shared registry.

When I built my image, I tagged it with the label latest. This means I marked the image as the most recent version, which is a common convention in Docker. Tagging an image as latest allows anyone pulling or deploying the image to always get the most up-to-date build without having to specify a version number. It’s especially useful when making frequent updates, since the same tag can be reused to point to the newest version of the image.

---

## Resolving Permission Issues

When I tried pulling my project buddy's container image for the first time, I saw the error 403 Forbidden. This was because Amazon ECR repositories are private by default, and I didn’t have the necessary permissions to access their repository. Without explicit access granted through IAM policies or repository permissions, Docker cannot authenticate and pull images from someone else's private ECR repo.

To resolve each other's permission errors, my buddy and I updated our ECR repository policies to include each other's Elastic Beanstalk role ARNs. This allowed our environments to access and pull the container images from each other’s repositories, fixing the access issues and ensuring the deployments worked successfully.


![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_74b90da414)

---

## Deploying the App

I used Elastic Beanstalk to deploy and run a containerized application in the cloud without having to manage the underlying infrastructure myself. When I set up an Elastic Beanstalk application, I configured settings like the container image to use, the port to expose, and the environment type. Elastic Beanstalk then automatically handled launching the necessary resources—like EC2 instances, load balancers, and networking—so my application could run smoothly and be accessed online.

While setting up for deployment, I created a new role for Elastic Beanstalk to use during the deployment process. The role has the permission to manage and launch EC2 instances, access logs, and interact with other AWS services required by the application. I gave Elastic Beanstalk access to ECR too, so it could securely pull the container image from Player A’s private ECR repository and deploy it within the environment.

The Dockerrun.aws.json file is a configuration file specifically used by AWS Elastic Beanstalk to deploy single-container Docker applications. My file tells Elastic Beanstalk to pull Player A’s container image from Amazon ECR, run it on port 80, and keep the application up to date by allowing image updates. It provides Elastic Beanstalk with all the necessary instructions to launch and manage the Docker container in the cloud.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_70ed85fa3)

---

## Resolving Deployment Issues

When I visited my environment's domain, I initially saw the error "This site can't be reached." This was because Elastic Beanstalk and the EC2 instances it launched didn’t have the correct permissions to access Player A’s private ECR repository. Although my IAM user had access through the ECR-Access role, that role isn’t used by the Elastic Beanstalk environment during deployment. To fix it, I needed to update the ECR repository’s policy to explicitly grant access to the service roles used by Elastic Beanstalk and then rebuild the environment so the changes could take effect.

To fix the permissions error, my buddy and I updated our ECR repository policies to explicitly allow access to the Elastic Beanstalk service roles used during deployment. My ECR repository's existing permission settings didn't work because they only allowed access to my IAM user, not the EC2 instances and service roles that Elastic Beanstalk actually uses. By adding permissions for the ecrInstanceRole and aws-elasticbeanstalk-service-role, we ensured that the environment could pull container images successfully. After updating the policy, we rebuilt the environment so the new settings could take effect.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-ecr_74b90da411)

---

---
