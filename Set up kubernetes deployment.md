<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up Kubernetes Deployment

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks2)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Set Up Kubernetes Deployment

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks2_45e6c3de5)

---

## Introducing Today's Project!

In this project , i will be cloning an app from the github and build a docker image and push the image into amazon ECR repository .

### Tools and concepts

I used Amazon EKS, Git, Docker, and Amazon ECR to build, containerize, and deploy a backend application to a Kubernetes cluster. Key steps include cloning the backend code from GitHub using Git, creating a container image with Docker, storing that image in Amazon ECR, and deploying the application to an Amazon EKS cluster. These tools and steps allowed me to automate and scale the deployment process in a cloud-native, production-ready environment.

### Project reflection

This project took me approximately 3 to 4 hours to complete. The most challenging part was resolving Docker permission issues for the ec2-user and troubleshooting EKS cluster creation errors. My favourite part was seeing the application come to life on a Kubernetes cluster after pushing the container image to ECR and deploying through EKS—it felt like all the components clicked into place.

Something new that I learnt from this experience was how Amazon EKS, Docker, and Amazon ECR work together in a real-world deployment pipeline. I gained a deeper understanding of how to containerize an application, push it to a container registry, and deploy it to a Kubernetes cluster—all within AWS. This gave me hands-on experience with cloud-native architecture and the confidence to manage infrastructure using industry-standard tools.

---

## What I'm deploying

To set up today's project, I launched a Kubernetes cluster. The process began with preparing my environment on an EC2 instance, ensuring all necessary tools like eksctl, kubectl, and the AWS CLI were installed and properly configured with the right IAM permissions. Once everything was in place, I created an EKS cluster using eksctl, specifying the cluster name, region (us-east-2), Kubernetes version (1.31), and defining a managed node group with t2.micro instances that could scale between one and three nodes.

During the creation, I initially ran into an issue where the cluster's CloudFormation stack already existed, likely from a previous failed or partial attempt. I resolved this by deleting the existing stack using eksctl delete cluster, which cleared out the conflicting resources. After that, I re-ran the cluster creation command successfully.

### I'm deploying an app's backend

Next, I retrieved the backend that I plan to deploy. An app's backend means the part of the application that handles logic, data processing, and communication with databases or external services — essentially, everything that powers the app behind the scenes. I retrieved the backend code by cloning a public GitHub repository using Git.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks2_1ebb86c71)

---

## Building a container image

Once I cloned the backend code, my next step is to build a container image of the backend. This is because containerizing the application bundles the code, runtime, libraries, and dependencies into a single, portable unit. This ensures that the backend runs reliably and consistently no matter where it’s deployed — whether on my local machine, an EC2 instance, or inside the Kubernetes cluster. Building the container image also prepares the app for easy scaling, updates, and management within the EKS environment.

When i ran Docker commands with sudo, they worked because sudo temporarily gave ec2-user root-level permissions. But if you want to run Docker commands without typing sudo every time—which is more convenient and considered good practice—i need to add ec2-user to the Docker group. This group has the rights to run Docker commands without needing root access each time.

To solve the permissions error , i added the user to the docker group.The Docker group is a special user group on Linux systems that grants permission to run Docker commands. By default, only the root user can execute Docker commands. When a user is added to the Docker group, they gain permission to interact with the Docker daemon directly, meaning they can run Docker commands without prefixing them with sudo.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks2_45e6c3de5)

---

## Container Registry

I'm using Amazon ECR in this project to securely store and manage the Docker container images of my backend application. ECR is a good choice for the job because it integrates seamlessly with AWS services like EKS, provides high availability, handles image versioning, and ensures fast, reliable access to container images during deployment—making it ideal for scalable, production-ready Kubernetes environments.

Container registries like Amazon ECR are great for Kubernetes deployment because they provide a centralized, secure place to store and manage container images. This makes it easy for Kubernetes to pull the exact version of an application image whenever needed, ensuring consistency across all deployed environments.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks2_l2m3n4o5)

---

## EXTRA: Backend Explained

After reviewing the app's backend code, I’ve learnt that it’s a lightweight Flask application designed to act as an API that connects to the Hacker News Search API. It takes a user-provided topic, sends a request to fetch related content, processes the results, and returns them in JSON format. The backend is containerized using a Dockerfile, which ensures consistent deployment, and its dependencies are clearly listed in requirements.txt to make setup straightforward. Overall, the backend is simple, efficient, and focused on fetching and delivering relevant news content based on user input.

### Unpacking three key backend files

The requirements.txt file lists all the Python libraries and packages that your backend application needs in order to run properly. It acts like a checklist for setting up the app’s environment, ensuring that anyone who wants to run the backend — whether on their own machine or inside a Docker container — installs the exact same dependencies.

The Dockerfile gives Docker instructions on how to build a container image for your backend application. It tells Docker what base image to start from, what dependencies to install, how to copy your code into the image, and how to run the app once the container starts.

The app.py file is the main code that powers the backend. It uses Flask to set up a route /contents/<topic>, which listens for requests. When someone visits that route, the app takes the topic from the URL, sends a request to the Hacker News Search API to find related content, and collects key details like ID, title, and URL. It then sends this data back as a formatted JSON response. In short, it connects user input to external data and delivers results through an API.

---

---
