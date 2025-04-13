## Question #1  
**Topic #1**

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

## Question #2  
**Topic #1**
 
 A company has an application that is running on Amazon EC2 instances. A solutions architect has standardized the company on a particular instance family and various instance sizes based on the current needs of the company.

The company wants to maximize cost savings for the application over the next 3 years. The company needs to be able to change the instance family and sizes in the next 6 months based on application popularity and usage.

**Which solution will meet these requirements MOST cost-effectively?**

**A. Compute Savings Plan**
**B. EC2 Instance Savings Plan**
**C. Zonal Reserved Instances**
**D. Standard Reserved Instances**

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

