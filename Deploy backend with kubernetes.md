<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy Backend with Kubernetes

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks4)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Deploy Backend with Kubernetes

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks4_6cfb382f2)

---

## Introducing Today's Project!

In this project, I will set up the backend of an app for deployment, install kubectl, and deploy the backend on a Kubernetes cluster because I want to learn how to manage and run containerized applications in a real-world, cloud-based environment. By working with Kubernetes and Amazon EKS, I’ll gain hands-on experience with modern DevOps practices. As part of a secret mission, I’ll also track my Kubernetes deployment using EKS to better understand how clusters and workloads are monitored and managed in production environments.

### Tools and concepts

I used Kubernetes, ECR, kubectl, Docker, and eksctl to deploy a containerized backend application on an Amazon EKS cluster. These tools worked together to build the app, store it in a container registry, and run it in a scalable cloud-native environment.

Key concepts include using manifests to define how Kubernetes should deploy and expose applications, pods as the smallest deployable units in a cluster, and Services to route traffic to the correct pods. I also learned how to use kubectl for cluster management and how ECR supports consistent deployment by serving as a centralized source for container images.

### Project reflection

This project took me approximately 3 to 4 hours to complete. The most challenging part was configuring IAM roles and permissions correctly to ensure the EC2 instance and EKS cluster could communicate and function properly — especially during cluster creation and access setup. My favourite part was seeing the backend application successfully deployed and running in the EKS console, knowing that all the components — Docker, ECR, Kubernetes, and the manifests — came together seamlessly to bring the app to life.

---

## Project Set Up

### Kubernetes cluster

In this step, I will launch an Amazon EKS cluster using the eksctl command because this cluster acts as the control plane where Kubernetes orchestrates the deployment, scaling, and management of my backend application.

The EKS cluster is the foundation of this entire project — it provides the environment where containers are scheduled on worker nodes, where networking is handled, and where my app’s backend can be reliably deployed and managed. Kubernetes uses this cluster to ensure that the app stays healthy, scales as needed, and can respond to traffic efficiently.

### Backend code

I retrieved backend code by cloning the GitHub repository shared by my team member using the git clone command. Pulling code is essential to this deployment because it gives me access to the actual source files needed to build the Docker image and deploy the application on Kubernetes. Without the backend code, I wouldn’t be able to containerize the app or define how it should run inside the EKS cluster. It’s the foundation for everything that follows in this deployment process.

### Container image

Once I cloned the backend code, I built a container image because Kubernetes needs a packaged version of the application — including all code, libraries, and dependencies — to deploy and run it consistently across the cluster. Without an image, it would be difficult for Kubernetes to create reliable containers, as it wouldn’t have a defined blueprint to follow. The container image ensures that every pod created by Kubernetes behaves exactly the same, whether it's in development, testing, or production.

I also pushed the container image to a container registry, which is Amazon Elastic Container Registry (ECR), because Kubernetes needs a reliable and accessible source to pull the image from during deployment. ECR facilitates scaling for my deployment because it allows the EKS cluster to pull the exact same image anytime it needs to spin up new pods, ensuring consistency across all replicas of my backend. This makes it easy to scale the application up or down without worrying about configuration drift or missing dependencies.

---

## Manifest files

Kubernetes manifests are configuration files written in YAML or JSON that define how Kubernetes should create and manage resources like Deployments, Services, and Pods. They act as blueprints that describe the desired state of your application — including which container images to use, how many replicas to run, and how to expose your app.

Manifests are helpful because they make deployment consistent, repeatable, and automated, allowing Kubernetes to set up and manage your application without manual intervention. This reduces errors, simplifies updates, and ensures your app runs reliably across different environments.


A Deployment manifest manages how Kubernetes should deploy, run, and maintain a specific number of identical copies (replicas) of your application. It ensures that your app stays running, scales up or down when needed, and updates safely through rolling deployments.

The container image URL in my Deployment manifest tells Kubernetes which version of the backend application to run by pointing to the exact container image stored in a registry like Amazon ECR. This ensures that every pod created by the Deployment uses the same image, leading to consistent and predictable behavior across the cluster.

A Service resource exposes a set of pods in Kubernetes so they can receive network traffic, either from within the cluster or from external sources. It acts as a stable endpoint that automatically routes requests to the appropriate pods, even if those pods are recreated or moved.

My Service manifest sets up a NodePort Service that makes the nextwork-flask-backend application accessible from outside the cluster by assigning a specific port on each node.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks4_b01876554)

---

## Backend Deployment!

To deploy my backend application, I used kubectl to apply my Deployment and Service manifests to the EKS cluster. First, I built a Docker image of the backend, pushed it to Amazon ECR, and then created a Deployment manifest that told Kubernetes how to run multiple replicas of that image. I also created a Service manifest to expose the backend so it could receive traffic. By running kubectl apply -f, I deployed both resources and successfully launched my backend on Kubernetes.

### kubectl

kubectl is the command-line tool used to interact with and manage resources inside a Kubernetes cluster, such as Deployments, Services, and Pods. I need this tool to apply manifest files, check the status of my app, and manage the lifecycle of Kubernetes resources after the cluster is created.

I can't use eksctl for the job because eksctl is mainly used for setting up and configuring the EKS cluster itself, not for deploying or managing applications within it. Once the cluster is running, kubectl is the go-to tool for deploying and operating apps inside that cluster.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks4_6cfb382f2)

---

## Verifying Deployment

My extension for this project is to use the EKS console to visually explore and monitor my Kubernetes cluster, including the deployed backend application, running pods, and Services. This helps me confirm that everything I deployed using kubectl is working as expected and gives me a more intuitive view of the cluster's state.

I had to set up IAM access policies because the EKS console requires proper permissions to view and interact with Kubernetes resources, such as Deployments and workloads. Without the right IAM policies, I wouldn’t be able to see or manage anything in the EKS UI.

Once I gained access into my cluster's nodes, I discovered pods running inside each node. Pods are the smallest deployable units in Kubernetes, and they act as wrappers that group one or more containers together so they can function as a single unit.

Containers in a pod share the same network space and storage, which allows them to communicate easily and work closely together. This design helps ensure efficient coordination between tightly coupled processes and is a core part of how Kubernetes manages and runs applications inside a cluster.

The EKS console shows you the events for each pod, where I could see a timeline of what actions Kubernetes took to start and manage the backend pod — such as pulling the container image, creating the container, starting it, and assigning networking resources. This validated that my backend pod was successfully created, the container image from ECR was pulled correctly, and the application started without errors, confirming that my Deployment and Service manifests were working as expected.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks4_3b391f873)

---

---
