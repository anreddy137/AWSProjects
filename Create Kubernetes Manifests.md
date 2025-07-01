<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create Kubernetes Manifests

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks3)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Create Kubernetes Manifests

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks3_b01876555)

---

## Introducing Today's Project!

In this project, I will set up a Deployment and Service manifest for my backend application using Kubernetes because this is essential for managing how my app runs and how users access it. The Deployment manifest ensures that Kubernetes knows how to launch and manage the backend container — including how many replicas to run and how to handle updates. The Service manifest makes the backend accessible by exposing it through a stable network endpoint. By exploring these manifest files, I’ll also deepen my understanding of Kubernetes concepts and how infrastructure is defined as code.

### Tools and concepts

I used Amazon EKS, eksctl, Docker, and Amazon ECR to build, containerize, and deploy a backend application in a Kubernetes cluster. Key concepts include using manifests to define how Kubernetes should deploy applications (with a Deployment manifest) and expose them (with a Service manifest). I also learned how to package an app using Docker, push it to a container registry (ECR), and run it in a scalable, cloud-based environment using EKS. These tools and concepts work together to automate and standardize app deployment across different environments.

### Project reflection

I did this project today because I wanted hands-on experience with deploying containerized applications using Kubernetes on AWS, which is a critical skill for modern cloud and DevOps workflows. This project helped me connect the dots between Docker, ECR, EKS, and Kubernetes manifests — all essential components of cloud-native development. It gave me a practical understanding of how to go from source code to a running application in the cloud using industry-standard tools. I now feel more confident in setting up and managing Kubernetes deployments in real-world scenarios.

This project took me approximately 60 to 90 minutes to complete.  My favourite part was seeing the application go live through Kubernetes after pushing the Docker image to ECR and applying the manifests — it was rewarding to watch all the pieces come together and know that the app was running in a fully managed, cloud-native environment.

---

## Project Set Up

### Kubernetes cluster

In this step, I will create my EKS cluster using eksctl from within the EC2 instance because this will provision a fully managed Kubernetes control plane along with worker nodes that can run my backend app.

### Backend code

I retrieved the backend that I plan to deploy by cloning the GitHub repository shared by my team member using Git. I navigated into the project folder using cd nextwork-flask-backend and listed the contents with ls to confirm that all necessary files were there.

The backend is the part of the application that handles logic, processes user requests, and communicates with other services or databases. Unlike the frontend, which users see and interact with, the backend runs behind the scenes to make everything work smoothly.

### Container image

Once I cloned the backend code, I built a container image because it allows Kubernetes to run consistent and repeatable instances of my backend across different environments. I used Docker to create the image by running the docker build command, which reads the instructions from the Dockerfile in the project directory. 

I also pushed the container image to a container registry, because Kubernetes needs a centralized and accessible place to pull the image from when deploying the application. Using Amazon ECR ensures that all nodes in my cluster can consistently access the latest version of the image without manual setup.

To push the image to ECR, I first tagged the image using the docker tag command, giving it a recognizable name and version (latest). Then, I used the docker push command to upload the image to my ECR repository. Once pushed, the image became available in the ECR console, ready for Kubernetes to pull and deploy across the cluster.

---

## Manifest files

Kubernetes manifests are YAML files that contain the configuration and instructions for how Kubernetes should deploy and manage your application. They define important details like which container image to use, how many replicas to run, what ports to expose, and how much memory or CPU to allocate.


A Kubernetes deployment manages how many copies (replicas) of my application should run, how to update them, and how to keep them running in the desired state. It ensures that if a pod fails or is removed, another one is automatically started to replace it.

The container image URL in my Deployment manifest tells Kubernetes which version of my backend application to run by pointing to the exact Docker image stored in my container registry (like Amazon ECR). This allows Kubernetes to pull and deploy the correct container every time a pod is created or restarted.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks3_b01876554)

---

## Service Manifest

A Service manifest in Kubernetes is a configuration file that tells Kubernetes how to expose your application and route traffic to the correct pods. It acts like a set of instructions for creating a Service — specifying things like which labels to match, which ports to listen on, and whether the app should be accessible only within the cluster or from the outside world.

My Service manifest sets up a LoadBalancer-type Kubernetes Service that exposes my backend application to external traffic. It tells Kubernetes to route incoming requests on port 80 to port 8080 on the pods labeled app: nextwork-flask-backend. This ensures that users outside the cluster can access the backend, and that traffic is correctly forwarded to the running application pods, regardless of their location within the cluster.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks3_b01876555)

---

## Deployment Manifest

---

---
