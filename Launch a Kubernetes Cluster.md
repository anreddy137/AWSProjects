<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launch a Kubernetes Cluster

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks1)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Launch a Kubernetes Cluster

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks1_e5f6g7h8)

---

## Introducing Today's Project!

In this project, I will launch and connect to an EC2 instance because it serves as the foundational infrastructure for setting up my Kubernetes environment. I will then create my very own Kubernetes cluster to orchestrate containerized applications efficiently. To ensure a streamlined and automated setup, I will monitor the cluster creation using AWS CloudFormation. For secure access and management, I will utilize an IAM access entry. Finally, I will test the resilience of the Kubernetes cluster to validate its ability to handle node failures and maintain high availability.

### What is Amazon EKS?

Amazon EKS (Elastic Kubernetes Service) is a managed service that makes it easier to run Kubernetes on AWS by handling the complex setup of the control plane, networking, and security for you. In today’s project, I used EKS to create and manage a Kubernetes cluster where containerized applications can run reliably and scale automatically. By leveraging tools like eksctl and IAM roles, I was able to launch the cluster, configure node groups, and securely access and monitor the environment — all while simplifying what would otherwise be a complex, manual process.

### One thing I didn't expect

One thing I didn’t expect in this project was how much AWS CloudFormation is working behind the scenes when creating the EKS cluster. I knew eksctl simplifies the process, but seeing the multiple CloudFormation stacks managing the cluster and node group infrastructure gave me a deeper appreciation of the automation happening under the hood.

### This project took me...

This project took me about 45 to 60 minutes in total. The part that took the longest was setting up the correct IAM roles and permissions to allow the EC2 instance and my user to interact with the EKS cluster securely. Troubleshooting permission errors and configuring the aws-auth ConfigMap required careful attention.

---

## What is Kubernetes?

Kubernetes is a container orchestration platform that automates the deployment, scaling, and management of containerized applications. In simple terms, it ensures that containers are running where they should, restarts them if they crash, and scales them up or down based on traffic. People use Kubernetes because it takes away the complexity of manually managing containers—especially in large-scale environments—so developers can focus more on building features and less on operational overhead.

I used eksctl to create a Kubernetes cluster on Amazon EKS. The create cluster command I ran defined key configuration details such as the cluster name, region, number of worker nodes, and the instance type for those nodes. This command also automatically created the required VPC, subnets, and IAM roles needed for the cluster to run successfully. By using eksctl, I simplified what would otherwise be a complex, multi-step setup process into a single, declarative command.

I initially ran into two errors while using eksctl. The first one was because my EC2 instance did not have the required IAM role attached, so it lacked permission to create EKS resources—this resulted in an AccessDeniedException. The second one was because I had not configured the AWS CLI with the correct region and credentials, which caused eksctl to fail when attempting to interact with AWS services.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks1_ff9bfc221)

---

## eksctl and CloudFormation

In this project, I observed that eksctl automatically provisions several networking resources such as a VPC, subnets, route tables, security groups, NAT gateways, and internet gateways. These are critical components that create a private and secure network for the Kubernetes cluster—allowing pods to communicate internally and securely access the internet when needed. While it's possible to use the default VPC, it often requires manual configuration to meet the specific networking needs of Kubernetes. Using eksctl simplifies this by creating an isolated, production-ready VPC setup tailored for EKS out of the box.

In this project, I noticed that two CloudFormation stacks were created: one for the EKS cluster and another for the node group. The first stack, eksctl-network-eks-cluster-cluster, provisions the core infrastructure for the Kubernetes control plane, including the VPC, subnets, IAM roles, and the EKS cluster itself. The second stack is specifically for the node group, which contains the EC2 instances that serve as worker nodes to run the containers.

CloudFormation separates these stacks to simplify management and troubleshooting—so if, for example, something goes wrong with the node group, it can be fixed or recreated independently without affecting the entire cluster setup. Before proceeding, I waited for the main cluster stack to reach CREATE_COMPLETE status before reviewing the Events tab of the node group stack to monitor its deployment.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks1_w3e4r5t6)

---

## The EKS console

I had to create an IAM access entry in order to allow my IAM user or role to interact with the EKS cluster using kubectl. An access entry is a permission mapping that grants specific IAM users or roles the ability to perform Kubernetes actions by associating them with Kubernetes RBAC roles.

I set it up by editing the aws-auth ConfigMap using kubectl. This involved mapping my IAM role to the system:masters group within Kubernetes, which gives full administrative access to the cluster. This step is crucial because, by default, only the IAM entity that created the cluster has permissions, and any additional users must be explicitly authorized.

It took around 15–20 minutes to create my cluster. Since I’ll create this cluster again in the next project of this series, maybe this process could be sped up if I automate the setup using a predefined eksctl configuration file or a script. That way, I won’t have to manually input all the parameters each time, and the setup will be more consistent and efficient.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks1_e5f6g7h8)

---

## EXTRA: Deleting nodes

This is because EKS worker nodes are actually EC2 instances that run your container workloads. When you create a node group with eksctl, it provisions EC2 instances under the hood, and those instances join your Kubernetes cluster as nodes. So, even though you're working with Kubernetes, the underlying compute resources still live in EC2.

Desired size is the number of nodes you want your node group to have running at any given time. Minimum and maximum sizes are helpful for autoscaling—they set the lower and upper limits so your cluster can automatically scale down or up based on demand, ensuring you have enough resources without overspending.

When I deleted my EC2 instances manually, the Kubernetes cluster eventually recognized that those nodes were no longer available and marked them as ‘NotReady’ or removed them from the node list. This is because the EKS control plane constantly monitors the health of nodes, and when nodes disappear without proper cordoning or draining, Kubernetes updates its state to reflect the loss. However, if autoscaling is enabled, new nodes may be automatically launched to replace the deleted ones to maintain the desired capacity.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eks1_q7r8s9t0)

---

---
