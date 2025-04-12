## Question #: 7
### Topic #: 1 - Design Resilient Architectures

**Question:**  
A company has an aging network-attached storage (NAS) array in its data center. The NAS array presents SMB shares and NFS shares to client workstations. The company does not want to purchase a new NAS array. The company also does not want to incur the cost of renewing the NAS array’s support contract. Some of the data is accessed frequently, but much of the data is inactive.

A solutions architect needs to implement a solution that migrates the data to Amazon S3, uses S3 Lifecycle policies, and maintains the same look and feel for the client workstations. The solutions architect has identified AWS Storage Gateway as part of the solution.

**Which type of storage gateway should the solutions architect provision to meet these requirements?**

**A.** Volume Gateway  
**B.** Tape Gateway  
**C.** Amazon FSx File Gateway  
**D.** Amazon S3 File Gateway

---

> 🔘 **Check Answer**

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
