<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App with Docker

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eb)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_c4df13c84)

---

## Introducing Today's Project!

### What is Docker?

Docker is a tool that lets you package your application along with everything it needs to run—like code, dependencies, and system tools—into a single, portable container. This makes sure your app runs the same way everywhere, whether it's on your laptop, a server, or in the cloud.

In today’s project, I used Docker to:

Create a Dockerfile that defines how to build my containerized web app.

Build a Docker image that includes my index.html and the environment needed to serve it.

Test the app locally using Docker to make sure it works before deployment.

Deploy the container to AWS Elastic Beanstalk, so it can run live on the web for anyone to see.

Docker made the whole process clean, consistent, and scalable!

### One thing I didn't expect...

One thing I didn't expect in this project was how smooth and fast the deployment process could be using Elastic Beanstalk with Docker. I thought setting up a live environment in the cloud would be complicated and take a long time, but once everything was packaged correctly, the deployment happened with just a few clicks—and my updated app was live in seconds. That was a pleasant surprise!

### This project took me...

This project took me approximately 1 to 2 hours. The most challenging part was making sure the Dockerfile and app files were correctly set up for deployment, especially when repackaging changes. It was most rewarding to see the app live on the web after deploying with Elastic Beanstalk—watching my updates appear in real time felt like a major win! 

---

## Understanding Containers and Docker

### Containers

Containers are lightweight, portable units that package an application along with everything it needs to run — including its code, libraries, dependencies, and runtime environment. They run consistently across different systems because they isolate the app from the host machine’s configuration.
They are useful because they solve the “it works on my machine” problem by ensuring that applications behave the same way in development, testing, and production environments, regardless of where they're running. This makes containers ideal for teams, cloud deployment, and building reliable, scalable apps.

A container image is a pre configured template that has all the configurations like the code, libraries, dependenciens and files.

### Docker

Docker is a platform that helps developers build, package, and run applications inside containers. It ensures that applications run consistently across different environments by bundling the code along with all its dependencies into a lightweight, isolated unit called a container.

Docker Desktop is a user-friendly application that runs on your local computer and provides the tools and interface to work with Docker. It lets you manage containers, build and store images, and monitor your Docker environment — all from a visual dashboard or command line. Together, Docker and Docker Desktop make it easy to develop, test, and deploy applications efficiently.

The Docker daemon is the background service that powers Docker — it’s the engine that actually runs your containers, builds images, and manages all Docker objects on your system. When you type Docker commands in the terminal or use Docker Desktop, those commands are sent to the Docker daemon, which then does the actual work of building, running, stopping, or removing containers.

In short, the Docker daemon is what makes Docker "go to work" behind the scenes, handling the heavy lifting while you interact through simple commands or a graphical interface.

---

## Running an Nginx Image

Nginx is  a web server , which means its a program that serves web pages to people on internet ,Engineers use nginx because it can handle traffic smoothly.

The command i ran to start a new container was docker  run -d -p 80:80 nginx.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_6245f5bb10)

---

## Creating a Custom Image

The Dockerfile is a set of instructions that tells Docker how to build a custom container image. It starts by using an existing image — in this case, nginx:latest — as the base, and then customizes it by replacing the default HTML file with my own index.html using the COPY command. The EXPOSE 80 line indicates that the container will handle web traffic on port 80. This file allows me to create a tailored image that serves my own content through a lightweight web server.

My Dockerfile tells Docker three things: first, it should use the latest version of the Nginx image as the base, which provides a lightweight web server to build on. Next, it copies my custom index.html file into the default directory where Nginx serves web content, replacing the default page with my own. Finally, it exposes port 80, which tells Docker that this container is intended to receive web traffic on that port. Together, these instructions let me create a custom web server container that displays my own content.

The command i used to build a custom image with my dockerfile was "docker build -t my-web-app . " here docker build command builds an image with with the name my-web-app , where '.' looks for a docker file in the current directory.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_4c741d1913)

---

## Running My Custom Image

There was an error when i ran my custom image because there was an image running at port 80. I resolved this by using the command docker ps --filter "publish=80" gives the name of the container image running on port 80 , so we can delete the containe

In this example, the container image is the blueprint that includes the Nginx server, my custom index.html file, and all necessary dependencies needed to run the web app. The container is the actual running instance created from that image — it’s the live software serving the webpage through the Nginx server, displaying my custom content to users.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_74b5c3d619)

---

## Elastic Beanstalk

Elastic Beanstalk is a service from AWS that simplifies the process of deploying and running applications in the cloud. Instead of manually setting up servers, configuring environments, and managing scaling, you just upload your application or container image — and Elastic Beanstalk takes care of the rest.

Deploying my custom image with elastic beanstalk took me around 20 minutes .

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_26d5573b23)

---

## Deploying App Updates

To learn how to deploy app updates with Elastic Beanstalk, I updated my app by adding a new <h2> subheading and an <img> tag to my index.html file. The subheading says "And here's a special image chosen by me", and the image is displayed using the src="" attribute with a style to control its size and layout.I verified those changes by opening the updated index.html file in my browser using "Open With → Google Chrome" from the Compute folder. I could clearly see the new header and the image displayed on the page, confirming the update was successful.

My app updates didn't show up in my live environment immediately because I needed to redeploy the latest version to Elastic Beanstalk. To deploy my changes, I only had to create a new zip file containing the updated index.html and the Dockerfile, then upload and deploy it through the Elastic Beanstalk console.

I went to the NextWorkApp-env environment, selected Upload and deploy, chose my new zip file, entered "Version Two" as the version label, and clicked Deploy. After waiting a few seconds, Elastic Beanstalk updated my environment, and I could see the latest version of my app live on the web. 

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-compute-eb_5b7034684)

---

---
