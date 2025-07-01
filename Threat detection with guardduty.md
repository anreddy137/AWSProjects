<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Threat Detection with GuardDuty

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-guardduty)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

---

## Introducing Today's Project!

### Tools and concepts

The services I used were AWS CloudShell, GuardDuty, CloudFormation, and S3.

Key concepts I learnt include how to exploit common web application vulnerabilities such as SQL injection and command injection, how sensitive IAM credentials can be exfiltrated through a misconfigured or vulnerable web server, and how attackers can use those stolen credentials to access AWS services like S3.

I also learned how GuardDuty uses anomaly detection and threat intelligence to identify suspicious activity in real time, such as unexpected usage of EC2 credentials by a different AWS account. Finally, I practiced securing my environment by cleaning up resources and understanding the impact of mismanaged access permissions.

### Project reflection

This project took me approximately several hours to complete. The most challenging part was carefully performing the command injection and correctly handling the stolen AWS credentials to simulate an attacker’s access without breaking the environment. It was most rewarding to see how GuardDuty detected the suspicious activity in real time, validating the effectiveness of AWS threat detection tools and deepening my understanding of cloud security vulnerabilities and defenses.

I did this project today to gain hands-on experience with real-world cloud security challenges, specifically understanding how vulnerabilities like SQL injection and command injection can be exploited, and how AWS tools like GuardDuty help detect and respond to such attacks. This project met my goals by giving me practical skills in both offensive and defensive cloud security, improving my ability to identify risks and protect AWS environments effectively.

---

## Project Setup

To set up for this project, I deployed a CloudFormation template that launches an intentionally vulnerable web application environment designed for security training and threat detection. The three main components are:

Web App Infrastructure — This includes an EC2 instance hosting the OWASP Juice Shop web app, along with networking resources such as a dedicated VPC and related networking components to isolate and manage traffic securely. The EC2 instance serves the app and processes incoming requests.

CloudFront Distribution and S3 Bucket — CloudFront is deployed to distribute the web app content globally and improve performance, while an S3 bucket stores sensitive data (like a text file with important information) that the web server can access, simulating a realistic data storage scenario.Amazon GuardDuty — GuardDuty is enabled to monitor and detect suspicious activity and threats within this environment, providing real-time security alerts as we simulate attacks on the web app.

The web app deployed is called OWASP Juice Shop, which is intentionally designed with security vulnerabilities. To practice my GuardDuty skills, I will simulate real-world cyberattacks by exploiting these vulnerabilities, such as stealing credentials and accessing sensitive data. Then, I will use GuardDuty to detect, analyze, and understand the alerts generated from these attacks, gaining hands-on experience in threat detection and incident response.

GuardDuty is a continuous security monitoring and threat detection service provided by AWS that uses machine learning, anomaly detection, and integrated threat intelligence to identify suspicious activity and potential threats within your AWS environment.

In this project, it will monitor the deployed vulnerable web application and associated resources to detect malicious behavior, such as unauthorized access attempts, reconnaissance activities, and data breaches, helping you understand how GuardDuty can protect cloud workloads by alerting you to real-world security threats.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_n1o2p3q4)

---

## SQL Injection

The first attack I performed on the web app is SQL injection, which means inserting malicious SQL code into an input field to manipulate the database query. SQL injection is a security risk because it can allow attackers to bypass authentication, access sensitive data, modify or delete database contents, and compromise the entire application’s security. In this case, by entering ' or 1=1;-- in the email field, I manipulated the login query to always return true, effectively bypassing the login check and gaining unauthorized access.

My SQL injection attack involved entering the string ' or 1=1;-- into the email field of the login page. This means I injected malicious SQL code that manipulates the database query to always evaluate as true, bypassing the authentication process and allowing unauthorized access to the web app without needing valid credentials.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_h1i2j3k4)

---

## Command Injection

Next, I used command injection, which is a security vulnerability where an attacker can insert and execute arbitrary commands on a server through an application’s input fields. The Juice Shop web app is vulnerable to this because it does not properly sanitize user input, allowing malicious scripts—like commands to retrieve sensitive data—to be run on the underlying EC2 instance hosting the app. This enables attackers to steal critical information such as the instance’s IAM credentials, escalating their access within the AWS environment.

To run command injection, I entered a specially crafted JavaScript payload into the username field that instructs the web server to execute commands on its own system. The script will contact the EC2 instance’s metadata service to retrieve its IAM security credentials and then expose those credentials in a publicly accessible location, allowing me (the attacker) to steal sensitive AWS access keys from the server.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_t3u4v5w6)

---

## Attack Verification

To verify the attack's success, I navigated to the JuiceShopURL found in the CloudFormation console’s Outputs tab, which pointed to the web app’s public interface where the injected malicious code had stored the stolen AWS credentials. The credentials page showed me a JSON file containing the AccessKeyId, SecretAccessKey, Session Token, and Expiration details—confirming that I had successfully extracted temporary AWS credentials from the vulnerable EC2 instance running the web app.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_x7y8z9a0)

---

## Using CloudShell for Advanced Attacks

The attack continues in CloudShell, because it allows me to simulate a hacker operating outside of the legitimate AWS environment by using the stolen credentials. Since CloudShell runs in a different AWS account context, using compromised credentials from the EC2 instance appears as unauthorized access. This helps trigger GuardDuty findings and demonstrates how AWS can detect suspicious behavior, such as credential misuse and data exfiltration from services like S3.

In CloudShell, I used wget to download the credentials.json file from the vulnerable web app, which contains the stolen AWS access credentials. This simulates an attacker retrieving sensitive information exposed through a command injection vulnerability.

Next, I ran a command using cat and jq to display and parse the contents of the credentials file in a readable JSON format. This allowed me to extract the AccessKeyId, SecretAccessKey, and SessionToken, which are necessary to authenticate and perform actions in the compromised AWS environment.

I then set up a profile, called stolen, to configure the AWS CLI with the stolen credentials and simulate unauthorized access to AWS services. I had to create a new profile because the default CloudShell profile uses the permissions of my logged-in IAM user, whereas this new profile allows me to act as an attacker using the compromised credentials. This separation is essential for mimicking a real-world intrusion and for observing whether GuardDuty can detect the suspicious activity coming from credentials that shouldn’t be used outside the EC2 instance.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_j9k0l1m2)

---

## GuardDuty's Findings

After performing the attack, GuardDuty reported a finding within a few minutes. Findings are detailed alerts generated by GuardDuty that highlight suspicious or potentially malicious activity within your AWS environment. Each finding includes information such as the type of threat detected, the resources affected, the severity level, and a timestamp, helping security teams quickly understand and respond to incidents.

GuardDuty's finding was called UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS, which means GuardDuty detected that credentials assigned to an EC2 instance (in this case, the web server running the Juice Shop app) were being used by another AWS account—something that should never happen under normal conditions.

Anomaly detection was used because GuardDuty continuously learns what typical behavior looks like for your resources. When the EC2 instance credentials were suddenly used from AWS CloudShell (a different AWS account), it stood out as unusual behavior. This deviation from the norm triggered the alert, helping identify a potential security breach before more damage could occur.

GuardDuty's detailed finding reported that the EC2 instance's IAM role credentials were being misused. Specifically, the credentials were used by a different AWS account (from AWS CloudShell) to access sensitive resources in the original account, such as an S3 bucket containing private information.

The finding included:

Resource affected: The IAM role tied to the EC2 instance hosting the Juice Shop app.

Action performed: An object (the secret-information.txt file) was retrieved from the S3 bucket.

Location and IP address: It showed that the activity originated from an AWS service (CloudShell) in the same region, but under a different AWS account, indicating credential exfiltration.This type of finding highlights a severe security breach, flagged as UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS, and is classified as high severity due to the sensitive nature of credentials being used from an unauthorized source. It demonstrates GuardDuty’s effectiveness in anoma

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-guardduty_v1w2x3y4)

---

## Extra: Malware Protection

---
