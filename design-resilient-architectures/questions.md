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
- ExamTopics Discussion:  
  https://www.examtopics.com/discussions/amazon/view/100220-exam-aws-certified-solutions-architect-associate-saa-c03/

</details>

## Question #: 02
### Topic #: 1 - Design Resilient Architectures

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

## Question #: 22  
### Topic #: 2 - Design Resilient Architectures

**Question:**  
A company is moving its data management application to AWS. The company wants to transition to an event-driven architecture. The architecture needs to be more distributed and to use serverless concepts while performing the different aspects of the workflow. The company also wants to minimize operational overhead.

**Which solution will meet these requirements?**

**A.** Build out the workflow in AWS Glue. Use AWS Glue to invoke AWS Lambda functions to process the workflow steps.  
**B.** Build out the workflow in AWS Step Functions. Deploy the application on Amazon EC2 instances. Use Step Functions to invoke the workflow steps on the EC2 instances.  
**C.** Build out the workflow in Amazon EventBridge. Use EventBridge to invoke AWS Lambda functions on a schedule to process the workflow steps.  
**D.** Build out the workflow in AWS Step Functions. Use Step Functions to create a state machine. Use the state machine to invoke AWS Lambda functions to process the workflow steps.
