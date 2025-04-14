## Question #01  
### Topic #: 4 - Design Cost-Optimized Architectures

A company hosts a web application on multiple Amazon EC2 instances. The EC2 instances are in an Auto Scaling group that scales in response to user demand. The company wants to optimize cost savings without making a long-term commitment.

**Which EC2 instance purchasing option should a solutions architect recommend to meet these requirements?**

**A.** Dedicated Instances only  
**B.** On-Demand Instances only  
**C.** A mix of On-Demand Instances and Spot Instances  
**D.** A mix of On-Demand Instances and Reserved Instances  

<details>
<summary><strong>✅ Check Answer</strong></summary>

**Correct Answer: C. A mix of On-Demand Instances and Spot Instances**

**Explanation:**  
- **Spot Instances** offer significant cost savings (up to 90%) and are ideal for stateless, flexible, or fault-tolerant workloads.  
- **On-Demand Instances** provide reliability and are used for the baseline needs.  
- This mix allows the application to remain cost-efficient and scalable without committing to long-term contracts like Reserved Instances.

### 📚 Reference (Official AWS Documentation):
- [Auto Scaling Groups with Multiple Instance Types and Purchase Options – AWS Docs](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html)
- [Amazon EC2 Instance Purchasing Options – AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)

</details>

## Question #02  
### Topic #: 4 - Design Cost-Optimized Architectures

**Question:** 
 A company has an application that is running on Amazon EC2 instances. A solutions architect has standardized the company on a particular instance family and various instance sizes based on the current needs of the company.

The company wants to maximize cost savings for the application over the next 3 years. The company needs to be able to change the instance family and sizes in the next 6 months based on application popularity and usage.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Compute Savings Plan
**B.** EC2 Instance Savings Plan
**C.** Zonal Reserved Instances
**D.** Standard Reserved Instances

<details>
<summary><strong>✅ Check Answer</strong></summary>

**✅ Correct Answer: A. Compute Savings Plan**

### ✔ Why Compute Savings Plan?

| Requirement                              | Benefit with Compute Savings Plan |
|------------------------------------------|-----------------------------------|
| Maximize cost savings                    | Up to **66% discount** vs On-Demand pricing |
| Flexibility across instance families     | Applies to **any instance family**, size, OS, or region |
| Anticipating usage pattern changes       | Ideal for unpredictable workloads |
| Lower management overhead                | No manual reservations or tracking needed |

## ❌ Why not the other options?

- **B. EC2 Instance Savings Plan**
  - Locked to a specific **instance family** within a region.
  - Less flexible than Compute Savings Plan.

- **C. Zonal Reserved Instances**
  - Tied to a specific **Availability Zone**.
  - No flexibility to change instance types or zones.

- **D. Standard Reserved Instances**
  - Locked to specific **instance types and configurations**.
  - Most cost-effective only when workloads are very stable and predictable.

---

Let me know if you'd like this saved as a file or want to add a table of contents, diagrams, or more examples!

### 🔗 References:

- AWS Docs – [Amazon S3 File Gateway](https://docs.aws.amazon.com/filegateway/latest/filefsxw/what-is-file-gateway.html)  

</details>

## Question #: 03
### Topic #: 4 - Design Cost-Optimized Architectures

**Question:**  
A company collects data from a large number of participants who use wearable devices. The company stores the data in an Amazon DynamoDB table and uses applications to analyze the data. The data workload is constant and predictable. The company wants to stay at or below its forecasted budget for DynamoDB.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use provisioned mode and DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA). Reserve capacity for the forecasted workload.  
**B.** Use provisioned mode. Specify the read capacity units (RCUs) and write capacity units (WCUs).  
**C.** Use on-demand mode. Set the read capacity units (RCUs) and write capacity units (WCUs) high enough to accommodate changes in the workload.  
**D.** Use on-demand mode. Specify the read capacity units (RCUs) and write capacity units (WCUs) with reserved capacity.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **B. Use provisioned mode. Specify the read capacity units (RCUs) and write capacity units (WCUs).**

---

### 📘 Explanation:

Since the company’s workload is **constant and predictable**, the most **cost-effective** approach is to use **provisioned mode**. In this mode, you can manually define the required RCUs and WCUs to match the expected usage. This allows tighter control over costs and avoids overprovisioning.

#### ✅ Why Option B is Correct:
- **Provisioned mode** fits **predictable workloads**, offering the ability to reserve just enough capacity.
- Avoids the overhead of on-demand costs.
- Allows the company to **stay within budget** by avoiding unnecessary scaling or unpredictable usage charges.

#### 🚫 Why not the others?

- **A.** Incorrect: DynamoDB Standard-IA is meant for **infrequently accessed** data, but the data here is **frequently accessed**, so this storage class is not appropriate.
- **C.** Incorrect: On-demand mode auto-scales, which is better for unpredictable workloads, and may be **more costly** for consistent workloads.
- **D.** Incorrect: On-demand mode does **not** allow manual specification of RCUs/WCUs or use reserved capacity, so the suggestion is technically invalid.

---

### 🔗 References:

- AWS Docs – [DynamoDB Read/Write Capacity Modes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)  
- AWS Docs – [DynamoDB Table Classes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/table-class.html)  
</details>