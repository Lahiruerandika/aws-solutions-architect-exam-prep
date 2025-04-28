## Question #: 01

**Question:**  
A company has an aging network-attached storage (NAS) array in its data center. The NAS array presents SMB shares and NFS shares to client workstations. The company does not want to purchase a new NAS array. The company also does not want to incur the cost of renewing the NAS array’s support contract. Some of the data is accessed frequently, but much of the data is inactive.

A solutions architect needs to implement a solution that migrates the data to Amazon S3, uses S3 Lifecycle policies, and maintains the same look and feel for the client workstations. The solutions architect has identified AWS Storage Gateway as part of the solution.

**Which type of storage gateway should the solutions architect provision to meet these requirements?**

**A.** Volume Gateway  
**B.** Tape Gateway  
**C.** Amazon FSx File Gateway  
**D.** Amazon S3 File Gateway

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **D. Amazon S3 File Gateway**

---

### 📘 Explanation:

**Amazon S3 File Gateway** is the ideal choice for this scenario. It presents a file interface (NFS or SMB) to on-premises clients, but stores the actual data in **Amazon S3**. This meets the need to:

- Maintain the same interface (NFS/SMB) for client workstations.
- Use **S3 Lifecycle policies** to manage storage costs by transitioning older data to cheaper storage classes like **S3 Glacier**.
- Avoid purchasing new on-premises storage or renewing support contracts.

#### ✅ Why Option D is Correct:
- **S3 File Gateway** enables access to objects in Amazon S3 as files through standard NFS and SMB protocols.
- Files are cached locally for low-latency access and can be accessed by multiple clients.
- Works well for replacing legacy NAS systems and allows seamless migration.

#### 🚫 Why not the others?
- **A. Volume Gateway** exposes block storage (iSCSI), not suitable for file-based workloads.
- **B. Tape Gateway** is for backup/archive workflows using virtual tapes — not appropriate for regular file access.
- **C. Amazon FSx File Gateway** is not a valid service — likely a confusion with **Amazon FSx for Windows/Linux**, which is a managed file system, not a Storage Gateway type.

---

### 🔗 References:

- AWS Docs – [Amazon S3 File Gateway](https://docs.aws.amazon.com/filegateway/latest/filefsxw/what-is-file-gateway.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100220-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 02

**Question:**  
A company hosts a three-tier web application on Amazon EC2 instances in a single Availability Zone. The web application uses a self-managed MySQL database that is hosted on an EC2 instance to store data in an Amazon Elastic Block Store (Amazon EBS) volume. The MySQL database currently uses a 1 TB Provisioned IOPS SSD (io2) EBS volume. The company expects traffic of 1,000 IOPS for both reads and writes at peak traffic.

The company wants to minimize any disruptions, stabilize performance, and reduce costs while retaining the capacity for double the IOPS. The company wants to move the database tier to a fully managed solution that is highly available and fault tolerant.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with an io2 Block Express EBS volume.  
**B.** Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.  
**C.** Use Amazon S3 Intelligent-Tiering access tiers.  
**D.** Use two large EC2 instances to host the database in active-passive mode.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **B. Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.**

---

### 📘 Explanation:

#### ✅ Why Option B is Correct:
- **Amazon RDS** in **Multi-AZ deployment** provides high availability and fault tolerance.
- **General Purpose SSD (gp2)** volumes can provide **up to 3,000 IOPS** per volume, depending on
### ✅ Correct Answer: **B. Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.**

---

### 📘 Explanation:

#### ✅ Why Option B is Correct:
- **Amazon RDS** in **Multi-AZ deployment** provides high availability and fault tolerance.
- **General Purpose SSD (gp2)** volumes can provide **up to 3,000 IOPS** per volume, depending on the size (you get 3 IOPS per GB). A 1 TB gp2 volume can provide **3,000 IOPS**, which is enough to handle **1,000 IOPS** read/write traffic and allows for future growth up to **double the current workload**.
- This option also **reduces costs significantly** compared to using **Provisioned IOPS (io2)**.

#### 🚫 Why not the others?

- **A.** io2 Block Express is very high performance and low latency, but it's **more expensive** than gp2. Not needed for this IOPS level if cost is a concern.
- **C.** Amazon S3 Intelligent-Tiering is **not suitable for databases**, as it’s designed for object storage and archival—not live transactional workloads.
- **D.** Hosting a MySQL cluster on EC2 in an active-passive configuration increases operational complexity, lacks managed features, and is **not fault-tolerant by default** without additional setup and tooling.

---

### 🔗 References:

- AWS Docs – [Amazon RDS Multi-AZ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)  
- AWS Docs – [EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)  

</details>

## Question #: 03

**Question:**  
A company is moving its data management application to AWS. The company wants to transition to an event-driven architecture. The architecture needs to be more distributed and to use serverless concepts while performing the different aspects of the workflow. The company also wants to minimize operational overhead.

**Which solution will meet these requirements?**

**A.** Build out the workflow in AWS Glue. Use AWS Glue to invoke AWS Lambda functions to process the workflow steps.  
**B.** Build out the workflow in AWS Step Functions. Deploy the application on Amazon EC2 instances. Use Step Functions to invoke the workflow steps on the EC2 instances.  
**C.** Build out the workflow in Amazon EventBridge. Use EventBridge to invoke AWS Lambda functions on a schedule to process the workflow steps.  
**D.** Build out the workflow in AWS Step Functions. Use Step Functions to create a state machine. Use the state machine to invoke AWS Lambda functions to process the workflow steps.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Build out the workflow in AWS Step Functions. Use Step Functions to create a state machine. Use the state machine to invoke AWS Lambda functions to process the workflow steps.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- **AWS Step Functions** allow the creation of a **serverless, event-driven workflow** that coordinates components, ensuring minimal operational overhead.
- You can design a **state machine** that defines the sequence of steps in the workflow.
- **AWS Lambda** functions are invoked by Step Functions at each step, making the architecture **highly distributed, serverless, and event-driven**.
- This approach is **cost-effective**, **scalable**, and **requires minimal maintenance**.

#### 🚫 Why the other options are incorrect:

- **A.** AWS Glue is primarily for **ETL jobs**, not general event-driven workflow management.
- **B.** Running applications on EC2 instances **increases operational overhead**, which goes against the goal of using serverless concepts.
- **C.** EventBridge is good for **event routing**, but **it doesn't inherently model complex workflows** like Step Functions does. Scheduling is not the primary requirement here.

---

### 🔗 References:
- [AWS Step Functions Documentation](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)  
- [AWS Lambda Overview](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)  
- [FreeCram Discussion](https://www.freecram.net/question/Amazon.AWS-Solutions-Associate.v2023-10-17.q198/a-company-is-moving-its-data-management-application-to-aws-the-company-wants-to-transition-to-an-event-dr)

## Question #: 04  
### Topic #: 2 - Design Resilient Architectures

**Question:**  
A company hosts a multiplayer gaming application on AWS. The company wants the application to read data with sub-millisecond latency and run one-time queries on historical data.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Use Amazon RDS for data that is frequently accessed. Run a periodic custom script to export the data to an Amazon S3 bucket.  
**B.** Store the data directly in an Amazon S3 bucket. Implement an S3 Lifecycle policy to move older data to S3 Glacier Deep Archive for long-term storage. Run one-time queries on the data in Amazon S3 by using Amazon Athena.  
**C.** Use Amazon DynamoDB with DynamoDB Accelerator (DAX) for data that is frequently accessed. Export the data to an Amazon S3 bucket by using DynamoDB table export. Run one-time queries on the data in Amazon S3 by using Amazon Athena.  
**D.** Use Amazon DynamoDB for data that is frequently accessed. Turn on streaming to Amazon Kinesis Data Streams. Use Amazon Kinesis Data Firehose to read the data from Kinesis Data Streams. Store the records in an Amazon S3 bucket.
