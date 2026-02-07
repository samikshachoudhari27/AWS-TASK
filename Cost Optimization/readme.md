Cost Optimization – Explanation
1. Use Free-Tier Eligible Instances
I used AWS free-tier eligible EC2 instances such as t2.micro / t3.micro.
These instance types are:
Low-cost
Suitable for small and medium workloads
Ideal for learning and testing environments
This helps reduce infrastructure costs while still meeting application requirements.

2. Minimal Resource Usage
I allocated only necessary resources:
Minimal CPU and memory
Lightweight Docker containers
Containerization ensures:
Efficient resource utilization
No unnecessary services running on the EC2 instances
This prevents wasting resources and keeps costs low.

3. Auto Scaling to Avoid Over-Provisioning
I configured Auto Scaling Groups (ASG) to automatically adjust the number of EC2 instances.
Instances are:
Added only when demand increases
Removed when demand decreases
Scaling is based on CPU utilization, ensuring:
No idle instances running unnecessarily
Cost-effective scaling during low traffic periods
