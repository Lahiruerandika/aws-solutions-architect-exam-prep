## Question #1  
**Domain:** Design Secure Architectures

A company is building a mobile app on AWS. The company wants to expand its reach to millions of users. The company needs to build a platform so that authorized users can watch the company’s content on their mobile devices.

**What should a solutions architect recommend to meet these requirements?**

**A.** Publish content to a public Amazon S3 bucket. Use AWS Key Management Service (AWS KMS) keys to stream content.  
**B.** Set up IPsec VPN between the mobile app and the AWS environment to stream content.  
**C.** Use Amazon CloudFront. Provide signed URLs to stream content.  
**D.** Set up AWS Client VPN between the mobile app and the AWS environment to stream content.  

<details>
<summary><strong>✅ Check Answer</strong></summary>

**Correct Answer: C. Use Amazon CloudFront. Provide signed URLs to stream content**

### 🧠 Explanation:
- **Amazon CloudFront** is a content delivery network (CDN) that securely delivers data, videos, and applications with low latency.
- **Signed URLs** allow the company to **restrict access** to authorized users only, making them ideal for serving **private content** such as video streams to mobile apps.
- This approach scales easily to millions of users and provides both **security** and **performance**.

> ❌ Option A exposes content publicly, even with encryption.
> ❌ Options B & D are VPN solutions, which are not scalable or suitable for content delivery to a global user base.

### 📚 Reference (Official AWS Documentation):
- [Serving Private Content with Signed URLs and Cookies – Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-signed-urls.html)
- [Using CloudFront for Video Streaming – AWS](https://docs.aws.amazon.com/whitepapers/latest/video-streaming-cloudfront/video-streaming-cloudfront.html)
- [ExamTopics Discussion – Question #100130 (SAA-C03)](https://www.examtopics.com/discussions/amazon/view/100130-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>
