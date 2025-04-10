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

</details>
