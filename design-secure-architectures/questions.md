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
A company uses a 100 GB Amazon RDS for Microsoft SQL Server Single-AZ DB instance in the us-east-1 Region to store customer transactions. The company needs high availability and automatic recovery for the DB instance.

The company must also run reports on the RDS database several times a year. The report process causes transactions to take longer than usual to post to the customers’ accounts. The company needs a solution that will improve the performance of the report process.

**Which combination of steps will meet these requirements? (Choose two.)**

**A.** Modify the DB instance from a Single-AZ DB instance to a Multi-AZ deployment.  
**B.** Take a snapshot of the current DB instance. Restore the snapshot to a new RDS deployment in another Availability Zone.  
**C.** Create a read replica of the DB instance in a different Availability Zone. Point all requests for reports to the read replica.  
**D.** Migrate the database to RDS Custom.  
**E.** Use RDS Proxy to limit reporting requests to the maintenance window.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answers:  
**A. Modify the DB instance from a Single-AZ DB instance to a Multi-AZ deployment.**  
**C. Create a read replica of the DB instance in a different Availability Zone. Point all requests for reports to the read replica.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- Converting from **Single-AZ to Multi-AZ** improves **high availability and automatic recovery**, ensuring failover to a standby in case of instance failure.

#### ✅ Why C is Correct:
- Creating a **read replica** offloads the **reporting workload** from the primary DB, improving **transaction performance** on the main database.

#### 🚫 Why the others are incorrect:

- **B.** Restoring a snapshot is a **manual, time-consuming** process and not intended for regular reporting or HA.
- **D.** RDS Custom is for **legacy or highly specialized** configurations and doesn’t provide a direct benefit for HA or performance in this use case.
- **E.** RDS Proxy improves **connection pooling** and application scaling, but it does not directly improve **reporting performance** or manage scheduling for reports.

---

### 🔗 Reference:
- [Amazon RDS Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)  
- [Amazon RDS Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100300-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 06

**Question:**  
A company wants to restrict access to the content of one of its main web applications and to protect the content by using authorization techniques available on AWS. The company wants to implement a serverless architecture and an authentication solution for fewer than 100 users. The solution needs to integrate with the main web application and serve web content globally. The solution must also scale as the company’s user base grows while providing the lowest login latency possible.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use Amazon Cognito for authentication. Use Lambda@Edge for authorization. Use Amazon CloudFront to serve the web application globally.  
**B.** Use AWS Directory Service for Microsoft Active Directory for authentication. Use AWS Lambda for authorization. Use an Application Load Balancer to serve the web application globally.  
**C.** Use Amazon Cognito for authentication. Use AWS Lambda for authorization. Use Amazon S3 Transfer Acceleration to serve the web application globally.  
**D.** Use AWS Directory Service for Microsoft Active Directory for authentication. Use Lambda@Edge for authorization. Use AWS Elastic Beanstalk to serve the web application globally.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Use Amazon Cognito for authentication. Use Lambda@Edge for authorization. Use Amazon CloudFront to serve the web application globally.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **Amazon Cognito** provides a **cost-effective authentication** mechanism suitable for small user bases and easily scalable.
- **Lambda@Edge** enables **low-latency, geographically distributed authorization**, enforcing rules near the user.
- **Amazon CloudFront** provides **global content delivery**, enhancing speed and performance for users worldwide.
- This combination is **fully serverless**, **highly scalable**, and incurs **low operational costs**, especially for <100 users.

#### 🚫 Why the other options are incorrect:

- **B.** AWS Directory Service is **overkill and costly** for fewer than 100 users and isn't serverless.
- **C.** S3 Transfer Acceleration is for **upload performance**, not ideal for web app delivery. Lambda doesn't provide global low-latency like Lambda@Edge.
- **D.** AWS Directory Service and Elastic Beanstalk **add operational overhead** and cost, making it less suitable for a lightweight, serverless solution.

---

### 🔗 References:
- [Amazon Cognito Overview](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)  
- [Lambda@Edge](https://docs.aws.amazon.com/lambda/latest/dg/lambda-edge.html)  
- [CloudFront Global Delivery](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100341-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>


## Question #: 06

**Question:**  
A hospital is designing a new application that gathers symptoms from patients. The hospital has decided to use Amazon Simple Queue Service (Amazon SQS) and Amazon Simple Notification Service (Amazon SNS) in the architecture.

A solutions architect is reviewing the infrastructure design. Data must be encrypted at rest and in transit. Only authorized personnel of the hospital should be able to access the data.

**Which combination of steps should the solutions architect take to meet these requirements? (Choose two.)**

**A.** Turn on server-side encryption on the SQS components. Update the default key policy to restrict key usage to a set of authorized principals.  
**B.** Turn on server-side encryption on the SNS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals.  
**C.** Turn on encryption on the SNS components. Update the default key policy to restrict key usage to a set of authorized principals. Set a condition in the topic policy to allow only encrypted connections over TLS.  
**D.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.  
**E.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply an IAM policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B.** Turn on server-side encryption on the SNS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals.  
**D.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.

---

### 📘 Explanation:

#### ✅ Why B and D are Correct:
- **Server-side encryption using KMS** allows control of key usage and management, fulfilling compliance needs.
- **Applying key policies** restricts decryption access to only **authorized personnel**.
- **Setting TLS-only policies** ensures encryption **in transit**.
- This approach meets the requirements for **data encryption at rest and in transit** and restricts access based on hospital roles.

#### 🚫 Why the other options are incorrect:

- **A.** Uses the **default key policy**, which may not sufficiently restrict access to authorized personnel.
- **C.** Only updates **default key policy** and sets TLS condition but doesn’t enforce use of **customer managed KMS key**, which is required.
- **E.** IAM policies can help restrict actions, but **key policies** are the **preferred method** for fine-grained control over KMS keys.

---

### 🔗 References:
- [Amazon SQS Encryption](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html)  
- [Amazon SNS Encryption](https://docs.aws.amazon.com/sns/latest/dg/sns-server-side-encryption.html)  
- [Using AWS KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)  

</details>


## Question #: 07

**Question:**  
A company’s web application consists of an Amazon API Gateway API in front of an AWS Lambda function and an Amazon DynamoDB database. The Lambda function handles the business logic, and the DynamoDB table hosts the data. The application uses Amazon Cognito user pools to identify the individual users of the application. A solutions architect needs to update the application so that only users who have a subscription can access premium content.

**Which solution will meet this requirement with the LEAST operational overhead?**

**A.** Enable API caching and throttling on the API Gateway API.  
**B.** Set up AWS WAF on the API Gateway API. Create a rule to filter users who have a subscription.  
**C.** Apply fine-grained IAM permissions to the premium content in the DynamoDB table.  
**D.** Implement API usage plans and API keys to limit the access of users who do not have a subscription.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Implement API usage plans and API keys to limit the access of users who do not have a subscription.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- API Gateway **usage plans and API keys** allow control over API access by associating users with specific plans.
- Ideal for separating **subscription tiers** like free and premium users.
- It is **cost-effective** and **requires minimal operational overhead** to manage.
- API keys can be distributed to Cognito-authenticated users based on subscription status.

#### 🚫 Why the other options are incorrect:

- **A.** API caching and throttling enhance performance and limit traffic but **do not control access** based on subscription.
- **B.** AWS WAF is great for filtering **IP-based or pattern-based threats**, but not for **subscription-based user access control**.
- **C.** Fine-grained IAM is powerful but **adds complexity** and is not well-suited for **rapidly changing user subscription statuses**.

---

### 🔗 References:
- [API Gateway Usage Plans and API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html)  
- [Amazon Cognito Overview](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)  
- [AWS Lambda + API Gateway Patterns](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102128-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>