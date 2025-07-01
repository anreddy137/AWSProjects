<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will demonstrate how to secure data using AWS Key Management Service (KMS). The goal is to show how encryption protects sensitive information in the cloud, ensuring that only authorized users can access and work with the data.

We'll start by creating a KMS encryption key, then use that key to encrypt a DynamoDB table. After that, we'll add and retrieve data to confirm everything is working securely. Along the way, we'll also explore how AWS automatically blocks unauthorized access, and finally, we'll configure user permissions so only the right people can encrypt or decrypt the data.

By the end of this project, you’ll have a solid understanding of how to implement encryption using AWS KMS to protect data stored in DynamoDB.

### Tools and concepts

Services I used include AWS Key Management Service (KMS) for creating and managing encryption keys, Amazon DynamoDB for storing encrypted data, and AWS Identity and Access Management (IAM) for managing user permissions. Key concepts I learnt include encryption, key management and lifecycle, customer managed keys (CMKs) versus AWS managed keys, transparent data encryption, fine-grained access control through key policies, and cross-account key access. These concepts showed me how to securely protect data at rest while controlling who can encrypt, decrypt, and manage encryption keys.

### Project reflection

This project took me approximately 60 minutes to complete. The most challenging part was understanding and configuring the key policies correctly to ensure the right users had access without exposing the keys to unauthorized users. It was most rewarding to see how AWS KMS seamlessly protects sensitive data and enforces strict access control, especially when testing with the restricted test user—which really demonstrated the power of encryption in the cloud.

I did this project today because I wanted to deepen my understanding of how encryption works in AWS, specifically with KMS and DynamoDB, and to gain hands-on experience managing encryption keys and securing data at rest. This project met my goals by clearly demonstrating how to create and control encryption keys, enforce access policies, and verify secure access to encrypted data. It gave me practical skills that are essential for roles focused on cloud security and data protection.

---

## Encryption and KMS

Encryption is the process of converting plain, readable data into an unreadable format called cipher text using a mathematical algorithm and an encryption key. Companies and developers do this to protect sensitive information—such as customer data, passwords, or financial records—from unauthorized access, even if that data is intercepted or exposed.

Encryption keys are unique digital codes that guide the encryption and decryption process. Only users or systems with the correct key can decrypt the data and turn it back into its original, readable form. By using encryption and securely managing the keys—especially with tools like AWS KMS—organizations ensure their data remains private, secure, and compliant with regulations.

AWS KMS is Amazon Web Services' Key Management Service, a secure and fully managed service that allows you to create, control, and use encryption keys to protect your data across AWS services. It acts as a centralized vault where you can manage who has access to your keys, how they’re used, and when they’re rotated or deleted.

Key management systems are important because they help organizations keep sensitive data secure by making encryption easier to implement and manage. They also provide access control, auditing, and compliance tracking, ensuring that encryption keys don’t fall into the wrong hands and that usage is well-monitored—critical for maintaining data security and meeting regulatory standards.

Encryption keys are broadly categorized as symmetric and asymmetric. I set up a symmetric key because it uses a single key to both encrypt and decrypt data, making it faster and more efficient—especially when working with large volumes of data like those stored in a DynamoDB table. Since both the encryption and decryption processes rely on the same key, it's ideal for use cases where performance matters and access can be controlled through AWS Identity and Access Management (IAM).

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is a fully managed NoSQL database service offered by AWS. DynamoDB is designed for high performance at scale, allowing applications to store and retrieve any amount of data with low latency. It's a great choice for use cases like mobile apps, games, e-commerce platforms, and real-time analytics, where fast and flexible data access is critical.

Because DynamoDB automatically handles tasks like scaling, replication, and backups, developers can focus on building applications without worrying about infrastructure. And with KMS encryption enabled, the data stored in DynamoDB is not only fast to access but also secure at rest, protecting it from unauthorized access.

The different encryption options in DynamoDB include Amazon DynamoDB owned keys, AWS managed keys, and customer managed keys (CMKs). Their differences are based on who controls the key and how much visibility and access you have:

Amazon DynamoDB owned keys are fully managed by DynamoDB. You don’t see or control the key at all—it's used behind the scenes for basic encryption needs.

AWS managed keys are handled by AWS KMS. You have limited visibility and tracking, but AWS manages the key's lifecycle.

Customer managed keys (CMKs) are created and controlled by you through AWS KMS. You decide who can access them, when they’re used, and how they’re rotated or retired.

I selected the customer managed key option because it gives me full control over encryption, aligns with best practices for securing sensitive data, and lets me enforce custom access policies.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by using key policies and AWS IAM policies to define who can use the key and what actions they can perform with it—such as encrypting, decrypting, or managing the key itself. These permissions are enforced at the KMS level, meaning that even if a user has access to a resource like a DynamoDB table, they still won’t be able to read or write encrypted data unless they have explicit permission to use the KMS key. This separation of resource access and encryption key usage adds a strong layer of security and fine-grained control.

Despite encrypting my DynamoDB table, I could still see the table's items because I have the necessary permissions to use the KMS encryption key. DynamoDB uses transparent data encryption, which means it automatically decrypts the data for authorized users or applications. When I access the table, DynamoDB retrieves the encrypted data, decrypts it using the KMS key, and displays it in a readable format—all behind the scenes, without requiring any manual decryption. This ensures that data remains secure at rest while staying easily accessible to users with proper access.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to test access to an encrypted DynamoDB table without KMS permissions. The permission policies I granted this user are AmazonDynamoDBFullAccess, which allows full interaction with all DynamoDB resources, but not access to the KMS key used for encryption. This setup is intentional so I can observe how AWS restricts data access when the user doesn’t have decryption privileges, even though they can technically access the database service itself.

After accessing the DynamoDB table as the test user, I encountered an “AccessDeniedException” error because the test user does not have permission to use the KMS key for decryption. Even though the user has full access to DynamoDB, they are blocked from viewing the table’s items due to missing kms:Decrypt permissions.

This confirmed that AWS KMS is correctly enforcing encryption security, allowing only users with the appropriate KMS key permissions to access encrypted data. It also demonstrated how encryption and access control work together to protect sensitive data in AWS.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I added the test user as a key user in the KMS key policy through the AWS Management Console. My key’s policy was updated to explicitly allow the test user to perform key actions such as Encrypt, Decrypt, ReEncrypt, and GenerateDataKey. This grants the test user permission to use the key for cryptographic operations, enabling them to access and work with the encrypted data in DynamoDB securely.

Using the test user, I retried accessing the encrypted DynamoDB table by refreshing the items view. I observed that the table’s data was now visible without any access errors, which confirmed that the updated KMS key policy successfully granted the test user permission to decrypt and read the encrypted data. This verified that the key policy changes took effect and that the test user can securely access the database as intended.

Encryption secures data instead of just relying on traditional access control tools like user permissions or network restrictions. I could combine encryption with access control policies, authentication mechanisms, and network security to create multiple layers of defense. This way, even if someone bypasses one security measure, the encrypted data remains protected and unreadable without the proper decryption keys, providing stronger overall security.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-security-kms_feffb2fb8)

---

---
