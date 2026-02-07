1. Launch EC2 (Cost-Optimized Instance)
I launched an AWS EC2 instance using t2.micro / t3.micro, which is cost-optimized and suitable for lightweight applications.
These instance types are ideal because they:
Consume low resources
Are eligible for AWS Free Tier
I selected Amazon Linux as the operating system.
Security groups were configured to allow:
SSH (port 22) for remote access
Required application port for container access

2. Install Docker on EC2
After connecting to the EC2 instance via SSH, I installed Docker.
Docker was started and enabled so it runs automatically on system reboot.
Docker allows applications to run inside containers, ensuring consistency and easy deployment.

3. Run Containers on EC2
I pulled or built Docker images on the EC2 instance.
Containers were launched using Docker, mapping:
EC2 host ports to container ports
This made the application accessible using the EC2 public IP and exposed port.
Containers were configured to keep running reliably on the EC2 instance.
