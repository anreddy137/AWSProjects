<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Nithyasri Aleti  
**Email:** anreddy137@gmail.com

---

## Website Delivery with CloudFront

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, I will demonstrate how to host and distribute a static website using Amazon S3 and CloudFront, AWS’s global content delivery network. I'm doing this project to learn how to set up scalable, low-latency website delivery infrastructure, manage permissions between S3 and CloudFront, and understand how CDNs can dramatically improve performance and reliability. This knowledge is essential for roles that focus on cloud architecture, DevOps, and frontend performance optimization.

### Tools and concepts

Services I used were Amazon S3, Amazon CloudFront, and IAM (for permissions and access control). Key concepts I learnt include content delivery network (CDN), which improves website performance by caching content at global edge locations; origin access control (OAC), which securely grants CloudFront permission to access private S3 content; and bucket policies, which define who can access specific files in an S3 bucket. I also learned how to set up a static website, configure a CloudFront distribution, and compare performance between direct S3 hosting and CDN-powered delivery.

### Project reflection

This project took me approximately 2 to 3 hours to complete. The most challenging part was troubleshooting the access denied error and correctly setting up Origin Access Control (OAC) along with the necessary S3 bucket policy. It was most rewarding to see the website load successfully through the CloudFront distribution and notice the improved performance compared to direct S3 hosting, knowing that the content is now securely and efficiently delivered to users around the world.

I did this project today to learn how to deliver static website content securely and efficiently using Amazon S3 and CloudFront. My goal was to understand how a CDN like CloudFront improves performance, how to securely configure access between CloudFront and S3 using Origin Access Control, and how to compare it with basic S3 static hosting. This project absolutely met my goals—it gave me hands-on experience with content delivery, permissions management, and real-world performance optimization techniques that are crucial for modern cloud and DevOps roles.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to store the static files of my website, such as HTML, CSS, JavaScript, and images. The S3 bucket acts as the origin for CloudFront, providing a reliable and scalable location to host web content. I can't use CloudFront for this task alone because CloudFront is a content distribution service, not a storage service—it needs an origin like S3 to pull content from and deliver it globally with low latency.

The three files that make up my website are index.html, which defines the structure and content of the webpage; style.css, which controls the visual styling like colors, fonts, and layout; and script.js, which adds interactive behavior such as responding to clicks or form submissions. Together, these files create a functional and visually styled web page.

I validated that my website files work by opening the index.html file in my browser and checking that the webpage displayed correctly, with proper styling from style.css and interactive functionality provided by script.js. This confirmed that all the files were correctly linked and functioning as expected before uploading them to the S3 bucket.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is a content delivery network, which means it distributes web content through a global network of edge locations to deliver files like HTML, CSS, JavaScript, and images with low latency and high transfer speeds. Businesses and developers use CloudFront because it improves website performance by caching content closer to users, reduces the load on the origin server (such as S3), enhances availability, and provides built-in security features like DDoS protection and HTTPS support.

To use Amazon CloudFront, you set up distributions, which are configurations that define how and from where your content is delivered to users. I set up a distribution for my static website to ensure it loads quickly and reliably for users around the world. The origin is my S3 bucket where the website files—like index.html, style.css, and script.js—are stored. This distribution tells CloudFront to pull content from the S3 bucket, cache it at edge locations, and serve it to users with low latency.

My CloudFront distribution's default root object is index.html. This means that when someone visits the root URL of my website (like https://d1234.cloudfront.net/), CloudFront will automatically serve the index.html file stored in my S3 bucket. This setup ensures that users are directed to the main homepage of my site without needing to specify a file name in the URL.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because my S3 bucket is private by default, and I hadn't yet granted CloudFront permission to access its contents. Since CloudFront acts as a middle layer, it needs explicit read access to the objects in the S3 bucket in order to serve them to users. Without the proper permissions or an Origin Access Control configuration, CloudFront cannot retrieve the files, resulting in the error.

My distribution's origin access settings were set to public, meaning CloudFront was configured to fetch content directly from my S3 bucket without restricted access controls. This caused the access denied error because even though the origin access was public, the objects inside my S3 bucket were still private by default. CloudFront couldn't access those files until I explicitly updated the object permissions in S3 to make them publicly readable.

To resolve the error , we can just change the settings to origin access control.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

To resolve the error, I set up origin access control (OAC). OAC is a secure way to allow CloudFront to access my S3 bucket without making the bucket or its objects publicly accessible. It acts as a dedicated identity for CloudFront, so it can fetch content securely from the S3 bucket while keeping all files private from the public internet. This improves security by limiting access to only CloudFront and allows more control over how and when the content is accessed.

Once I set up my OAC, I still needed to update my bucket policy because S3 needs an explicit policy that allows access to CloudFront using that OAC. Without this policy, S3 still treats all incoming requests—even from CloudFront—as unauthorized, since the default bucket behavior is to deny all access. The policy update ensures S3 recognizes and accepts signed requests from CloudFront’s OAC.

Creating an OAC automatically gives me a policy I could copy, which grants CloudFront permission to access the objects in my S3 bucket using signed requests. This policy ensures that only CloudFront, through its trusted identity, can retrieve the content—while keeping the bucket and its files private from the public internet. It prevents unauthorized access and enables secure, seamless delivery of my website through the CloudFront distribution.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

---

## S3 vs CloudFront Load Times

Load time means the amount of time it takes for a website's content to fully appear and become usable in a user's browser. The load times for the CloudFront site were faster than the S3 site because CloudFront caches the website content at edge locations around the world, reducing the distance data needs to travel. In contrast, the S3 static website hosting serves files from a single AWS region, which can result in longer load times for users who are geographically far from that region.

A business would prefer CloudFront when performance, scalability, and global reach are priorities—such as serving customers across multiple regions, ensuring low latency, or needing enhanced security features like HTTPS, DDoS protection, and signed URLs. CloudFront is ideal for high-traffic websites, content-heavy platforms, or applications that require fast, reliable delivery worldwide.

S3 static website hosting might be sufficient when the website is simple, traffic is low to moderate, and the primary audience is located near the bucket’s region. It's a great fit for internal tools, prototypes, or region-specific informational sites where advanced caching and performance optimization aren't critical.

![Image](http://learn.nextwork.org/thoughtful_navy_swift_korimako/uploads/aws-networks-cloudfront_12verpuh)

---

---
