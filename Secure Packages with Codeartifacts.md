<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Packages with CodeArtifact

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codeartifact-updated)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Introducing Today's Project!

In this project, I will demonstrate how to integrate AWS CodeArtifact with a web application hosted on an EC2 instance. I'm doing this project to learn how to set up a secure and efficient private package repository using CodeArtifact, manage IAM permissions for access control, and enable my web app to pull and publish dependencies directly to and from the repository. This end-to-end setup will also help me understand how to use GitHub for version control and automate the deployment of code changes to my EC2-hosted application.

### Key tools and concepts

Services I used were Amazon EC2, AWS CodeArtifact, IAM (Identity and Access Management), GitHub, and Maven. Key concepts I learnt include how to configure an EC2 instance to host a Java web application, how to create and manage a private package repository using CodeArtifact, and how to securely connect services using IAM roles and policies. I also learned how Maven uses settings.xml and pom.xml to manage dependencies, and how to integrate a CodeArtifact repository into a CI/CD pipeline to ensure secure and consistent builds.

### Project reflection

This project took me approximately 3 to 4 hours to complete. The most challenging part was troubleshooting the 401 Unauthorized error, which required carefully verifying IAM role attachments, token generation, and settings in the settings.xml file. It was most rewarding to see the dependencies successfully populate in the CodeArtifact repository, confirming that the integration worked and that my CI/CD setup was functioning securely and efficiently.

This project is part three of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project within the next few days to continue progressing through the pipeline setup. I'm excited to build on what I've learned so far and dive deeper into automated deployments, continuous integration, and monitoring tools as part of the complete DevOps workflow.

---

## CodeArtifact Repository

CodeArtifact is a fully managed artifact repository service by AWS that allows you to securely store, publish, and share software packages used in your application development. Engineering teams use artifact repositories because they provide a centralized and reliable way to manage dependencies, ensuring that all developers and build systems use the same versions of packages. This improves build consistency, enhances security by controlling access to trusted packages, and supports collaboration through easy sharing of internal and external artifacts.

A domain is a top-level container in CodeArtifact that groups multiple repositories under a single organizational unit. It allows you to manage access control, permissions, and settings centrally, rather than configuring them individually for each repository. This makes it easier to enforce consistent security policies and streamline administration across teams and projects. My domain is nextwork-devops-domain, and it helps me manage all related repositories for my CI/CD pipeline efficiently by providing a unified place for policy and access management.

A CodeArtifact repository can have an upstream repository, which means it can pull packages from another repository if they aren't found locally. This allows seamless access to external dependencies without duplicating them in your own repository. My repository's upstream repository is maven-central-store, which connects my CodeArtifact repository to Maven Central, enabling it to fetch Java packages directly from the public Maven repository when needed.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## CodeArtifact Security

### Issue

To access CodeArtifact, we need an authorization token because CodeArtifact is a secure, private repository that requires authenticated access to manage and retrieve packages. This token acts as temporary credentials that allow Maven to connect to the repository on behalf of the EC2 instance. I ran into an error when retrieving a token because my EC2 instance didn't yet have the appropriate IAM permissions. Without these permissions, the instance cannot request or use the authorization token, blocking Maven from interacting with the CodeArtifact repository.

### Resolution

To resolve the error with my security token, I created a custom IAM policy that granted the necessary CodeArtifact permissions and attached it to a new IAM role. I then associated that IAM role with my EC2 instance. This resolved the error because the EC2 instance now had the correct permissions to request and retrieve a temporary authorization token from CodeArtifact, allowing Maven to securely access the repository.

It's security best practice to use IAM roles because they provide temporary, automatically rotated credentials to AWS resources like EC2 instances without the need to hard-code access keys or secrets. This minimizes the risk of credential leakage and ensures that permissions are managed centrally through policies. IAM roles also allow you to follow the principle of least privilege, giving only the necessary access for a specific task, and make it easier to audit and rotate permissions securely across your infrastructure.

---

## The JSON policy attached to my role

The JSON policy I set up grants permissions for the EC2 instance to interact with AWS CodeArtifact by allowing actions such as codeartifact:GetAuthorizationToken, codeartifact:GetRepositoryEndpoint, and codeartifact:ReadFromRepository. These permissions are necessary because they enable the instance to authenticate with CodeArtifact, retrieve the correct repository URL, and access packages from the repository. Without these permissions, Maven wouldn't be able to securely connect to CodeArtifact to download dependencies or upload artifacts.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using settings.xml

The settings.xml file configures Maven to connect securely to AWS CodeArtifact by specifying authentication details, repository endpoints, and mirror settings. It includes the authorization token under the <servers> tag, which allows Maven to authenticate with CodeArtifact. The <profiles> section defines which repositories Maven should use for downloading dependencies, and the <mirrors> section ensures Maven routes all package requests through CodeArtifact. Together, these configurations enable Maven to locate, authenticate, and retrieve project dependencies directly from the CodeArtifact repository, streamlining and securing the build process.

Compiling means converting your project's source code (written in Java, in this case) into bytecode that can be executed by the Java Virtual Machine (JVM). When you run the mvn compile command, Maven reads the pom.xml file to identify dependencies and build instructions, then uses the settings.xml file to determine where to fetch those dependencies from—such as your CodeArtifact repository. This process ensures that all necessary packages are downloaded, your code is validated, and compiled classes are generated in the target directory, preparing your app for execution or deployment.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## Verify Connection

After compiling, I checked the CodeArtifact repository nextwork-devops-cicd. I noticed that the dependencies required by my Java web app were successfully stored there. This confirmed that Maven was able to fetch the packages through CodeArtifact, and that the repository is now caching them for faster, more reliable future builds.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Uploading My Own Packages

---

---
