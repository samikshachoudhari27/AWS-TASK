1. Configure Application Load Balancer (ALB)
I configured an Application Load Balancer (ALB) to distribute incoming traffic across multiple EC2 instances.
The ALB:
Works at Layer 7 (HTTP/HTTPS).
Routes traffic based on rules such as URL paths or ports.
I created:
A Target Group with EC2 instances running the application.
Health checks to ensure traffic is sent only to healthy instances.
This improves:
High availability
Fault tolerance
Application reliability

2. Attach Auto Scaling Group (ASG)
I created an Auto Scaling Group (ASG) and attached it to the ALB.
The ASG:
Automatically manages the number of EC2 instances.
Launches new instances when demand increases.
Terminates instances when demand decreases.
The EC2 instances in the ASG use
A Launch Template with preconfigured AMI, instance type, and startup scripts (Docker + app).

4. Scale Based on CPU Utilization
I configured scaling policies based on CPU utilization:
Scale out (add instances) when CPU usage exceeds a defined threshold (for example, >70%).
Scale in (remove instances) when CPU usage drops below a threshold.
This ensures:
Optimal performance during high traffic
Cost savings during low traffic
