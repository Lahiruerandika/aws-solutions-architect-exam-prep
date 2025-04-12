## Question #: 01
### Topic #: 2 - Design High-Performing Architectures

**Question:**  
A company is designing the network for an online multi-player game. The game uses the UDP networking protocol and will be deployed in eight AWS Regions. The network architecture needs to minimize latency and packet loss to give end users a high-quality gaming experience.

**What solution will meet these requirements?**

**A.** Set up a transit gateway in each Region. Create inter-Region peering attachments between each transit gateway.  
**B.** Set up AWS Global Accelerator with UDP listeners and endpoint groups in each Region.  
**C.** Set up Amazon CloudFront with UDP turned on. Configure an origin in each Region.  
**D.** Set up a VPC peering mesh between each Region. Turn on UDP for each VPC.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **B. Set up AWS Global Accelerator with UDP listeners and endpoint groups in each Region.**

---

### 📘 Explanation:

AWS **Global Accelerator** is specifically designed for applications that require **low latency**, **minimal packet loss**, and **high availability** — exactly what online multiplayer games demand. It uses the **AWS global network infrastructure**, allowing user requests to enter the AWS backbone at the nearest edge location and travel over the optimized network path.

#### Benefits of Global Accelerator:
- Supports **UDP** traffic (critical for real-time gaming).
- Automatically routes traffic to the **nearest healthy endpoint** in the designated Region.
- Provides **regional failover**, improving fault tolerance.
- Minimizes **internet hops**, improving performance compared to standard public internet routing.

---

### 🔗 References:

- AWS Global Accelerator official documentation:  
  https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-what-is-global-accelerator.html

- Related discussion on ExamTopics:  
  https://www.examtopics.com/discussions/amazon/view/100130-exam-aws-certified-solutions-architect-associate-saa-c03/  
  https://www.examtopics.com/discussions/amazon/view/100197-exam-aws-certified-solutions-architect-associate-saa-c03/

</details>

## Question #: 02
### Topic #: 2 - Design High-Performing Architectures

**Question:**  
A company hosts a serverless application on AWS. The application uses Amazon API Gateway, AWS Lambda, and an Amazon RDS for PostgreSQL database. The company notices an increase in application errors that result from database connection timeouts during times of peak traffic or unpredictable traffic. The company needs a solution that reduces the application failures with the least amount of change to the code.

**What should a solutions architect do to meet these requirements?**

**A.** Reduce the Lambda concurrency rate.  
**B.** Enable RDS Proxy on the RDS DB instance.  
**C.** Resize the RDS DB instance class to accept more connections.  
**D.** Migrate the database to Amazon DynamoDB with on-demand scaling.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **B. Enable RDS Proxy on the RDS DB instance.**

---

### 📘 Explanation:

When using AWS Lambda with Amazon RDS, a common challenge is **managing database connections**, especially during **traffic spikes**. Each Lambda invocation can potentially open a new database connection, quickly exhausting the connection pool of the RDS instance.

#### ✅ Why RDS Proxy is the best choice:
- **Manages and pools connections** efficiently.
- Helps avoid **connection exhaustion** during high concurrency.
- Requires **minimal code changes** (in most cases, just updating connection settings).
- **Improves database scalability and resilience** for serverless apps.

#### 🚫 Why not the others?
- **A. Reduce Lambda concurrency rate** – Might limit scalability and won't solve the root problem.
- **C. Resize RDS instance** – Helps temporarily but doesn't solve connection storming from Lambda.
- **D. Migrate to DynamoDB** – A large change in architecture; not minimal or quick.

---

### 🔗 References:

- AWS Docs – [Using Amazon RDS Proxy with AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-rds.html)  
- AWS Docs – [Amazon RDS Proxy](https://docs.aws.amazon.com/rds/latest/UserGuide/rds-proxy.html)  
- ExamTopics Discussions:  
  https://www.examtopics.com/discussions/amazon/view/83199-exam-aws-certified-solutions-architect-associate-saa-c02/


</details>

## Question #: 03
### Topic #: 2 - Design High-Performing Architectures

**Question:**  
A company has a Java application that uses Amazon Simple Queue Service (Amazon SQS) to parse messages. The application cannot parse messages that are larger than 256 KB in size. The company wants to implement a solution to give the application the ability to parse messages as large as 50 MB.

**Which solution will meet these requirements with the FEWEST changes to the code?**

**A.** Use the Amazon SQS Extended Client Library for Java to host messages that are larger than 256 KB in Amazon S3.  
**B.** Use Amazon EventBridge to post large messages from the application instead of Amazon SQS.  
**C.** Change the limit in Amazon SQS to handle messages that are larger than 256 KB.  
**D.** Store messages that are larger than 256 KB in Amazon Elastic File System (Amazon EFS). Configure Amazon SQS to reference this location in the messages.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **A. Use the Amazon SQS Extended Client Library for Java to host messages that are larger than 256 KB in Amazon S3.**

---

### 📘 Explanation:

Amazon SQS has a **hard limit of 256 KB** for message size. If your application needs to send **larger messages (up to 2 GB)**, you must store the message payload **externally** and send a reference to it via SQS.

#### ✅ Why Option A is Correct:
- AWS provides the **Amazon SQS Extended Client Library for Java**, which seamlessly stores large message payloads in **Amazon S3**, and sends a pointer (reference) through SQS.
- This **minimizes code changes** and integrates smoothly into existing SQS-based Java applications.
- Allows messages up to **2 GB** in size (well above the 50 MB needed).

#### 🚫 Why not the others?
- **B. EventBridge** is not designed for large message payloads (limit is 256 KB as well).
- **C.** You **cannot change the 256 KB limit** on SQS — it’s a hard service limit.
- **D.** Amazon SQS cannot directly reference Amazon EFS files in its message body — this would require **custom logic** and **significant code changes**.

---

### 🔗 References:

- AWS Docs – [Amazon SQS Extended Client Library for Java](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html)  
- ExamTopics Discussion:  
  https://www.examtopics.com/discussions/amazon/view/100202-exam-aws-certified-solutions-architect-associate-saa-c03/

</details>

## Question #: 04
### Topic #: 2 - Design High-Performing Architectures

**Question:**  
A transaction processing company has weekly scripted batch jobs that run on Amazon EC2 instances. The EC2 instances are in an Auto Scaling group. The number of transactions can vary, but the baseline CPU utilization that is noted on each run is at least 60%. The company needs to provision the capacity 30 minutes before the jobs run.

Currently, engineers complete this task by manually modifying the Auto Scaling group parameters. The company does not have the resources to analyze the required capacity trends for the Auto Scaling group counts. The company needs an automated way to modify the Auto Scaling group’s desired capacity.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Create a dynamic scaling policy for the Auto Scaling group. Configure the policy to scale based on the CPU utilization metric. Set the target value for the metric to 60%.  
**B.** Create a scheduled scaling policy for the Auto Scaling group. Set the appropriate desired capacity, minimum capacity, and maximum capacity. Set the recurrence to weekly. Set the start time to 30 minutes before the batch jobs run.  
**C.** Create a predictive scaling policy for the Auto Scaling group. Configure the policy to scale based on forecast. Set the scaling metric to CPU utilization. Set the target value for the metric to 60%. In the policy, set the instances to pre-launch 30 minutes before the jobs run.  
**D.** Create an Amazon EventBridge event to invoke an AWS Lambda function when the CPU utilization metric value for the Auto Scaling group reaches 60%. Configure the Lambda function to increase the Auto Scaling group’s desired capacity and maximum capacity by 20%.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **C. Create a predictive scaling policy for the Auto Scaling group. Configure the policy to scale based on forecast. Set the scaling metric to CPU utilization. Set the target value for the metric to 60%. In the policy, set the instances to pre-launch 30 minutes before the jobs run.**

---

### 📘 Explanation:

**Predictive scaling** in EC2 Auto Scaling uses machine learning to forecast future traffic trends and automatically adjusts capacity ahead of time. Since the batch jobs are **weekly and follow a consistent pattern**, predictive scaling is **ideal** because it can pre-launch instances **30 minutes before the jobs start**, without manual intervention or needing additional resources to analyze trends.

#### ✅ Why Option C is Correct:
- Predictive scaling is designed to detect patterns and launch instances in advance, minimizing latency or startup lag.
- Minimal operational overhead — no manual intervention is required once it's configured.
- Supports the use case where usage trends (like scheduled jobs) are predictable and repetitive.

#### 🚫 Why not the others?
- **A.** Dynamic scaling only reacts to real-time metrics and does not pre-launch instances.
- **B.** Scheduled scaling requires manual updates and is slightly less efficient than predictive.
- **D.** EventBridge + Lambda adds unnecessary complexity and overhead.

---

### 🔗 References:

- AWS Docs – [Predictive Scaling for EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-predictive-scaling.html)  
- ExamTopics Discussion:  
  [https://www.examtopics.com/discussions/amazon/view/100204-exam-aws-certified-solutions-architect-associate-saa-c03/](https://www.examtopics.com/discussions/amazon/view/100204-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>