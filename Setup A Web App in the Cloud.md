<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

In today’s project, I will launch an EC2 instance, connect to it remotely using VS Code, and set up a Java-based web application using Maven. I’ll install the necessary tools like Java and Maven on the instance, generate a basic web app, and even try editing the code directly from the terminal to experience what it’s like without the help of an IDE. This project will give me hands-on experience with server setup, remote development, and Java web app creation — and a deeper appreciation for tools like VS Code that make development much easier.

### Key tools and concepts

Services I used were Amazon EC2 for creating a virtual server, Apache Maven for generating the structure of a Java web application, and Amazon Corretto 8 for running Java. I also used VS Code with the Remote - SSH extension to connect to and edit files on the EC2 instance.

Key concepts I learnt include setting up a cloud-based development environment, using Maven to scaffold a Java web app, understanding the difference between static HTML and dynamic JSP files, and the contrast between editing code in an IDE versus a terminal-based editor like Nano. These concepts helped me understand how real-world cloud development workflows operate from setup to deployment.

### Project reflection

One thing I didn't expect in this project was how different and challenging it felt to edit code directly in the terminal using a tool like Nano, compared to using a full-featured IDE like VS Code. It really highlighted how much more efficient and comfortable development can be with the right tools — and gave me a deeper appreciation for why developers rely so heavily on IDEs in their workflow.

This project took me approximately 60 minutes to complete. The most challenging part was managing remote connections and configuring permissions correctly for secure SSH access, especially when connecting VS Code to the EC2 instance. It was most rewarding to see the custom Java web application come to life and be able to edit and deploy it using both the terminal and an IDE — it really made all the setup feel worthwhile.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project in the series to continue integrating more automation, testing, and deployment stages. Each step is bringing me closer to understanding how modern software delivery works in real-world cloud environments.

---

## Launching an EC2 instance

I started this project by launching an EC2 instance because I needed a virtual server in the cloud to build, run, and test my web application. Hosting the development environment on EC2 allows me to work entirely in the cloud, which mirrors real-world deployment scenarios and helps ensure my app runs consistently in a production-like environment. It also gives me full control over the setup, tools, and resources needed for developing my Java web app.

### I also enabled SSH

SSH is a secure protocol that allows you to remotely access and control another computer over a network. It encrypts your connection to keep data safe while you interact with the remote machine through a terminal.

I enabled SSH so that I could securely connect to my EC2 instance from my local computer and manage it directly using command-line tools or a code editor like VS Code. This allows me to install software, run commands, and build my web app on the remote server as if I were working on it locally.

### Key pairs

A key pair lets us securely access the EC2 instance , it has two halves one is a public key that AWS keeps and the user will be storing his own private key .

Once I set up my key pair , AWS automatically downloaded the private key to my desktop

---

## Set up VS Code

VS Code is a lightweight, powerful code editor developed by Microsoft that supports many programming languages and tools. It’s widely used by developers for writing, editing, and debugging code, and it comes with features like syntax highlighting, extensions, Git integration, and built-in terminal support.

I installed VS Code to create a more efficient and user-friendly development environment while working on my EC2 instance. It allows me to write, edit, and manage code remotely, connect to the server via SSH, and use integrated tools like the terminal and extensions — all from one place. This makes building and maintaining my cloud-based web application faster and easier compared to working entirely from the command line.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is somethings that lets us communicate with our operating system with some instructions. i ran my first command to navigate it to the folder that has the key pair.

I also updated my private key's permissions by running the chmod 400 command on the key file, which restricts access so that only the file's owner can read it. This step is required by SSH to ensure the key is secure and not accessible to others. Without this permission setting, SSH would block the connection to my EC2 instance for security reasons.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

To connect to my EC2 instance, I ran the SSH command using my private key file and the instance’s public IPv4 DNS address. This established a secure connection between my local computer and the EC2 server, allowing me to access and work inside the remote instance directly from my terminal.

### This command required an IPv4 address

A server's IPV4 DNS is its public address on the internet that allows other devices to locate and connect to it, similar to how a website URL points to a specific server. In the case of an EC2 instance, the Public IPv4 DNS is what I use from my local machine to securely connect to the server via SSH or access any web applications running on it. It acts like the EC2 instance’s "name tag" on the internet, making it easier to connect without needing to remember its numeric IP address.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

Apache Maven is a build automation and project management tool used primarily for Java applications. It helps developers easily compile code, manage dependencies, run tests, and package applications. Maven uses a configuration file called pom.xml to define project structure, libraries, and plugins, making it easier to build and manage complex Java projects in a consistent and repeatable way.

Apache Maven is a build automation and project management tool used primarily for Java applications. It helps developers easily compile code, manage dependencies, run tests, and package applications. Maven uses a configuration file called pom.xml to define project structure, libraries, and plugins, making it easier to build and manage complex Java projects in a consistent and repeatable way.

Java is a widely used programming language that allows developers to build all kinds of applications, from simple websites to complex enterprise systems. It’s known for being platform-independent, meaning code written in Java can run on any device that has the Java Virtual Machine (JVM). In this project, Java is essential because it's the foundation that powers the web app we’re building, and it's also required for tools like Maven to work properly.

Java is required in this project because it is the programming language used to build and run the web application we’re developing on the EC2 instance. Additionally, the build tool we’re using — Apache Maven — depends on Java to function. Without Java installed, we wouldn’t be able to compile, build, or run the application code, making it a critical part of the project setup.

---

## Create the Application

I generated a Java web app using the command
mvn archetype:generate -DartifactId=nextwork-web-project -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
This command told Maven to create a new web application project named nextwork-web-project using a predefined web app template. By setting interactive mode to false, Maven installed everything automatically without prompting me for additional input.

I installed Remote - SSH, which is a VS Code extension that lets you securely connect to and work on remote servers directly from the editor. I installed it to easily access and edit the files on my EC2 instance without needing to use the terminal for everything. It provides a smooth and user-friendly development experience by allowing me to browse folders, open files, and use VS Code’s features — like syntax highlighting and extensions — while working in a cloud-based environment.

Configuration details required to set up a remote connection include the Host (which is the public IPv4 DNS of the EC2 instance), the User (which is usually ec2-user for Amazon Linux), and the IdentityFile (which is the path to my .pem private key file). These details allow VS Code’s Remote - SSH extension to authenticate and securely connect to the EC2 instance, enabling remote access to edit and manage files directly from the editor.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

Using VS Code's file explorer, I could see the entire directory structure of my EC2 instance, including the folder for my Java web app (nextwork-web-project) and its subfolders like src, webapp, and WEB-INF. I was able to easily navigate through the project files, open and edit the HTML and Java files, and view configuration files like pom.xml — all from a clean, organized interface without needing to use terminal commands.

Two of the project folders created by Maven are src and webapp, which serve as the main directories for organizing the code and content of a Java web application.

The src folder (short for “source”) contains the Java source code, such as servlet classes and other backend logic. The webapp folder holds the web-facing content, like HTML, CSS, and JSP files that are served to users when they visit the web app. These folders help keep the project well-structured and separate the backend logic from the frontend interface.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

index.jsp is a file used in Java web applications that serves as the entry point for displaying web pages. It's similar to an HTML file because it contains markup to structure and present content on the web. However, unlike HTML, index.jsp can also include Java code, allowing it to generate dynamic content based on user input, backend logic, or database data. This makes it more powerful for building interactive and personalized web experiences, which is why Java needs to be installed on the EC2 instance to properly run and render JSP files.

I edited index.jsp by opening it in VS Code through the Remote - SSH connection to my EC2 instance. I replaced the placeholder content with a custom message that included my name using basic HTML. After making the changes, I saved the file using Command/Ctrl + S. This allowed me to update the web page content that my Java web app will display when it runs.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

An alternative to using IDEs is editing files directly in the terminal using a built-in text editor. To edit index.jsp, I ran the command nano index.jsp, which opened the file in the Nano text editor right inside the terminal. This allowed me to navigate and make changes using just my keyboard, without the need for a graphical interface.

Compared to using an IDE, editing index.jsp in the terminal felt more limited and less user-friendly. Without features like syntax highlighting, autocomplete, and a file explorer, it was harder to navigate and spot mistakes. I had to rely entirely on keyboard shortcuts, which took some getting used to.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-vscode_a3324ad41)

---

---
