<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Continuous Integration with CodeBuild

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codebuild-updated)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codebuild-updated_35588a47)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up and configure an AWS CodeBuild project from scratch, connect it to a GitHub repository, and define the build process using a buildspec.yml file. I'm doing this project to learn how to automate the build and test phases of a CI/CD pipeline using AWS CodeBuild. This will help me understand how to streamline application development by integrating code changes, running automated tests, and generating build artifacts—all in a secure and scalable way.

### Key tools and concepts

Services I used were AWS CodeBuild, Amazon S3, AWS CodeArtifact, IAM, and GitHub. Key concepts I learnt include how to automate the build and test phases of a CI/CD pipeline using CodeBuild, how to securely connect CodeBuild to a GitHub repository, and how to define build instructions using a buildspec.yml file. I also learned how to manage build artifacts using S3, grant proper IAM permissions for CodeBuild to access CodeArtifact, and troubleshoot common CI errors. These skills are essential for creating reliable, automated workflows in modern DevOps environments.

### Project reflection

This project took me approximately 2.5 to 3 hours to complete. The most challenging part was troubleshooting the second build failure caused by missing IAM permissions for CodeBuild to access CodeArtifact. It was most rewarding to see the build succeed and the generated artifact appear in the S3 bucket, confirming that my CI pipeline was working as intended from source code to deployable package.

This project is part four of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project soon to integrate CodeDeploy and automate the deployment of my web application to EC2. With the build phase now automated, the next step will focus on continuous deployment—ensuring that every successful build gets smoothly and reliably delivered to the production environment.

---

## Setting up a CodeBuild Project

CodeBuild is a continuous integration service, which means it automates the process of compiling source code, running tests, and packaging applications every time code is pushed to a repository. Engineering teams use it because it helps catch errors early, ensures consistent builds, and eliminates the need to manually manage build servers. With CodeBuild, teams can scale their development efforts, increase reliability, and streamline their CI/CD pipelines—all while paying only for the compute time they use. 

My CodeBuild project's source configuration means the location where CodeBuild will pull the source code from to run the build. This includes the codebase, configuration files like buildspec.yml, and anything else needed for compilation and testing. I selected GitHub as my source provider because my Java web application's code is hosted there, and I want CodeBuild to automatically fetch the latest version of the code for each build.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codebuild-updated_fewgrhte)

---

## Connecting CodeBuild with GitHub

There are multiple credential types for GitHub, like Personal Access Tokens and OAuth Apps. I used GitHub App because it’s the most secure and user-friendly option. With GitHub App, AWS manages the authentication and connection on my behalf, eliminating the need to manually handle tokens or rotate credentials. It provides a seamless setup, better integration with AWS services, and minimizes security risks—making it the recommended choice for most CI/CD pipelines.

The service that helped connect AWS CodeBuild with my GitHub repository is AWS CodeConnections. It established a secure and managed link between my AWS environment and GitHub, allowing CodeBuild to access my repository without needing to manually manage tokens or credentials. This streamlined the authentication process and ensured a reliable integration between my CI/CD pipeline and source code.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codebuild-updated_a7c98e2d)

---

## CodeBuild Configurations

### Environment

My CodeBuild project's Environment configuration means defining the settings for how and where the build runs. It includes settings like the provisioning model (I chose On-demand), which means AWS will spin up build environments only when needed and shut them down afterward—helping reduce costs. It also includes the operating system (e.g., Amazon Linux), the runtime (e.g., Java and Maven), and the environment image managed by AWS to ensure compatibility and security during the build process.

### Artifacts

Build artifacts are the output files generated during the build process—such as compiled code, packaged applications (like .jar or .war files), and test reports. They're important because these artifacts are what get deployed to production or tested further in the CI/CD pipeline. My build process will create these packaged files from my Java web app using Maven. To store them, I created an S3 bucket named nextwork-devops-cicd-yourname, which will serve as a centralized, durable, and accessible storage location for these build artifacts.

### Packaging

When setting up CodeBuild, I also chose to package artifacts in a Zip file because it helps reduce the overall file size, making uploads to S3 faster and more efficient. This compression saves storage space and lowers data transfer costs. Additionally, it keeps all build output neatly organized in a single file, which simplifies the deployment process and makes it easier to share or move the artifacts as needed. Packaging everything into one Zip file ensures that nothing gets missed and makes post-build tasks more straightforward.

### Monitoring

For monitoring, I enabled CloudWatch Logs, which is a powerful AWS service that captures and stores logs generated during the build process. It helps me track every step of the build, see which commands were executed, view their outputs, and quickly identify any errors if the build fails. I set a custom group name /aws/codebuild/nextwork-devops-cicd to keep logs organized and easily searchable, especially as more projects are added to the environment. This setup ensures clear visibility into my CI pipeline and makes debugging and auditing much more efficient.

---

## buildspec.yml

My first build failed because CodeBuild couldn’t find a buildspec.yml file in the root directory of my GitHub repository. A buildspec.yml file is needed because it tells CodeBuild exactly what commands to run during each phase of the build—such as installing dependencies, compiling the code, running tests, and packaging artifacts. Without this file, CodeBuild has no instructions to follow, so it cannot proceed with the build process. This failure is expected and is a normal part of setting up a CI pipeline. We'll fix it by creating and committing a proper buildspec.yml file.M

The first two phases in my buildspec.yml file are install and pre_build. In the install phase, I specify the runtime environment—for example, setting up Java 8 so CodeBuild knows what language and tools to use. The pre_build phase is where I run commands that need to happen before building starts, such as retrieving a CodeArtifact authorization token to securely download dependencies.

The third phase in my buildspec.yml file is build, where I use Maven to compile my Java web application and perform tasks like resolving dependencies and running tests.

The fourth phase in my buildspec.yml file is post_build, which is where I finalize the build by packaging the compiled code into a .war file, preparing it for deployment. This phase also defines what will be saved as artifacts, such as the target/*.war file, which is the final output of the build process.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codebuild-updated_35588a47)

---

## Success!

My second build also failed, but with a different error that said CodeBuild couldn't access the settings.xml file. This usually indicates that CodeBuild doesn’t have permission to retrieve packages from CodeArtifact. To fix this, I need to update the IAM role associated with my CodeBuild project and attach a policy that grants it permissions such as codeartifact:GetAuthorizationToken, codeartifact:GetRepositoryEndpoint, and codeartifact:ReadFromRepository. This will allow CodeBuild to authenticate with CodeArtifact and download the necessary dependencies during the build process.

To resolve the second error, I attached the codeartifact-nextwork-consumer-policy to my CodeBuild service role. This policy gave CodeBuild the necessary permissions to authenticate with CodeArtifact and access the settings.xml file along with any required dependencies. When I built my project again, I saw the build progress successfully through all phases, confirming that CodeBuild could now securely retrieve packages from CodeArtifact and complete the CI process without errors.

To verify the build, I checked my S3 bucket named nextwork-devops-cicd. Inside the bucket, I found the artifact file named nextwork-devops-cicd-artifact.zip. Seeing the artifact tells me that the build process successfully compiled and packaged my Java web app, completed all phases without errors, and properly uploaded the final output. When I downloaded and inspected the zip file, I found the nextwork-web-project.war file inside, confirming that the build produced the expected deployable artifact.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-devops-codebuild-updated_d9cc6191)

---

## Automating Testing

---

---
