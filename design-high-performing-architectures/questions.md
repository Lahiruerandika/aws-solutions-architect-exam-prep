## Question #: 3
### Topic #: 2 - Design High-Performing Architectures

**Question:**  
A company is designing the network for an online multi-player game. The game uses the UDP networking protocol and will be deployed in eight AWS Regions. The network architecture needs to minimize latency and packet loss to give end users a high-quality gaming experience.

**What solution will meet these requirements?**

**A.** Set up a transit gateway in each Region. Create inter-Region peering attachments between each transit gateway.  
**B.** Set up AWS Global Accelerator with UDP listeners and endpoint groups in each Region.  
**C.** Set up Amazon CloudFront with UDP turned on. Configure an origin in each Region.  
**D.** Set up a VPC peering mesh between each Region. Turn on UDP for each VPC.

---

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
