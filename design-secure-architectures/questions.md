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

## Question #: 03

**Question:**  
A company uses Amazon API Gateway to run a private gateway with two REST APIs in the same VPC. The BuyStock RESTful web service calls the CheckFunds RESTful web service to ensure that enough funds are available before a stock can be purchased. The company has noticed in the VPC flow logs that the BuyStock RESTful web service calls the CheckFunds RESTful web service over the internet instead of through the VPC. A solutions architect must implement a solution so that the APIs communicate through the VPC.

**Which solution will meet these requirements with the FEWEST changes to the code?**

**A.** Add an X-API-Key header in the HTTP header for authorization.  
**B.** Use an interface endpoint.  
**C.** Use a gateway endpoint.  
**D.** Add an Amazon Simple Queue Service (Amazon SQS) queue between the two REST APIs.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Use an interface endpoint.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Private API Gateway** endpoints can be accessed via **interface VPC endpoints (powered by AWS PrivateLink)**.
- This ensures that communication between services **stays within the VPC**, avoiding traversal over the public internet.
- Using an interface endpoint enables **internal routing** between the REST APIs with **minimal code or architecture changes**.

#### 🚫 Why not the others?

- **A.** Adding an API key does not affect network routing. It is only for authorization.
- **C.** Gateway endpoints are used for **S3 and DynamoDB** only, not API Gateway.
- **D.** Introducing SQS adds unnecessary complexity and asynchronous communication, which is **not needed** and would **require major changes to the application logic**.

---

### 🔗 References:

- AWS Docs – [Accessing Private APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-private-apis.html)  
- AWS Docs – [Interface VPC Endpoints (AWS PrivateLink)](https://docs.aws.amazon.com/vpc/latest/privatelink/endpoint-services-overview.html) 
- ExamTopics Discussion – Question (https://www.examtopics.com/discussions/amazon/view/100238-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>

## Question #: 04

**Question:**  
A company stores confidential data in an Amazon Aurora PostgreSQL database in the ap-southeast-3 Region. The database is encrypted with an AWS Key Management Service (AWS KMS) customer managed key. The company was recently acquired and must securely share a backup of the database with the acquiring company’s AWS account in ap-southeast-3.

**What should a solutions architect do to meet these requirements?**

**A.** Create a database snapshot. Copy the snapshot to a new unencrypted snapshot. Share the new snapshot with the acquiring company’s AWS account.  
**B.** Create a database snapshot. Add the acquiring company’s AWS account to the KMS key policy. Share the snapshot with the acquiring company’s AWS account.  
**C.** Create a database snapshot that uses a different AWS managed KMS key. Add the acquiring company’s AWS account to the KMS key alias. Share the snapshot with the acquiring company’s AWS account.  
**D.** Create a database snapshot. Download the database snapshot. Upload the database snapshot to an Amazon S3 bucket. Update the S3 bucket policy to allow access from the acquiring company’s AWS account.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Create a database snapshot. Add the acquiring company’s AWS account to the KMS key policy. Share the snapshot with the acquiring company’s AWS account.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- Since the Aurora database is **encrypted with a customer managed KMS key**, sharing the snapshot with another AWS account **requires that account to have decrypt permissions** on the KMS key.
- You must **update the KMS key policy** to allow the acquiring company’s AWS account access.
- Once that’s done, you can **share the snapshot** using Amazon RDS's snapshot sharing feature.

#### 🚫 Why the others are incorrect:

- **A.** You **cannot copy an encrypted snapshot to an unencrypted one** for Aurora — it’s not supported for security reasons.
- **C.** Changing the KMS key or alias alone doesn't help. Sharing access requires **explicit permissions** on the key, not just the alias.
- **D.** You **cannot download RDS or Aurora snapshots** directly like regular files. There is **no mechanism to "download" a snapshot** and upload it to S3.

---

### 🔗 Reference:
- AWS Docs – [Sharing encrypted snapshots](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_ShareSnapshot.html)
- AWS Docs – [Granting cross-account access to KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html)

</details>

## Question #: 05

**Question:** 

**Question:**  
A company stores confidential data in an Amazon Aurora PostgreSQL database in the ap-southeast-3 Region. The database is encrypted with an AWS Key Management Service (AWS KMS) customer managed key. The company was recently acquired and must securely share a backup of the database with the acquiring company’s AWS account in ap-southeast-3.

**What should a solutions architect do to meet these requirements?**

**A.** Create a database snapshot. Copy the snapshot to a new unencrypted snapshot. Share the new snapshot with the acquiring company’s AWS account.  
**B.** Create a database snapshot. Add the acquiring company’s AWS account to the KMS key policy. Share the snapshot with the acquiring company’s AWS account.  
**C.** Create a database snapshot that uses a different AWS managed KMS key. Add the acquiring company’s AWS account to the KMS key alias. Share the snapshot with the acquiring company’s AWS account.  
**D.** Create a database snapshot. Download the database snapshot. Upload the database snapshot to an Amazon S3 bucket. Update the S3 bucket policy to allow access from the acquiring company’s AWS account.
