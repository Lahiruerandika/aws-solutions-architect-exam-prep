## Question #: 01  

**Question:** 
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


## Question #: 02

**Question:**  
A hospital needs to store patient records in an Amazon S3 bucket. The hospital’s compliance team must ensure that all protected health information (PHI) is encrypted in transit and at rest. The compliance team must administer the encryption key for data at rest.

**Which solution will meet these requirements?**

**A.** Create a public SSL/TLS certificate in AWS Certificate Manager (ACM). Associate the certificate with Amazon S3. Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.  
**B.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with S3 managed encryption keys (SSE-S3). Assign the compliance team to manage the SSE-S3 keys.  
**C.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.  
**D.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Use Amazon Macie to protect the sensitive data that is stored in Amazon S3. Assign the compliance team to manage Macie.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- The `aws:SecureTransport` condition ensures **encryption in transit** by only allowing HTTPS requests.
- **SSE-KMS** encrypts data at rest using **customer-managed AWS KMS keys**, allowing fine-grained access control and auditability.
- This setup meets **HIPAA compliance requirements** for protecting PHI.
- The **compliance team can control the KMS keys**, satisfying the requirement for key management.

#### 🚫 Why not the others?

- **A.** ACM public certificates cannot be directly associated with S3 buckets for upload/download access; S3 uses HTTPS natively.
- **B.** SSE-S3 does encrypt at rest but **does not allow customer-managed key administration**, which the compliance team requires.
- **D.** Amazon Macie helps **detect sensitive data** but does **not encrypt** it — and doesn’t replace KMS or bucket policies for encryption controls.

---

### 🔗 References:

- AWS Docs – [Protecting Data Using Server-Side Encryption with KMS keys (SSE-KMS)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingKMSEncryption.html)  
- AWS Docs – [Protecting Data In Transit](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html#encrypt-in-transit)  
- AWS Docs – [Bucket Policy Examples: Enforcing HTTPS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html#example-bucket-policies-use-case-ssl)

</details>