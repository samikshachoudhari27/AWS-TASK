1. AWS EC2 Deployment – Explanation
First, I deployed the application on AWS EC2 using a cost-optimized instance.
I launched an EC2 instance using t2.micro / t3.micro, which is eligible for the free tier and suitable for lightweight applications.
I selected Amazon Linux as the OS and configured:
Security Group to allow required ports (like 22 for SSH and application port, e.g., 5000/80).
I connected to the EC2 instance using SSH.


2. Installing Docker on EC2
After logging into the EC2 instance, I installed Docker using Linux package commands.
I started the Docker service and enabled it so that:
Docker starts automatically when the EC2 instance reboots.
I also added the EC2 user to the Docker group to run Docker commands without sudo.

3. Docker Setup – Application Containerization
a) Application Files :- app.py
This is the main application file (for example, a Python/Flask app).
It contains the logic to run the web application and listens on a specific port.

requirements.txt
This file lists all Python dependencies required for the application (like Flask).




b) Dockerfile
I created a Dockerfile to define how the application container is built:
Used a lightweight Python base image.
Copied app.py and requirements.txt into the container.
Installed dependencies using pip.
Exposed the required application port.
Defined the command to run the application when the container starts.


4. Running the Application Using Docker
I built the Docker image using the Dockerfile.
Then, I ran the Docker container:
Mapped the container port to the EC2 instance port.
This allows external users to access the app via EC2’s public IP.

Example concept (no commands needed in explanation):
Host Port → Container Port
EC2 Public IP + Port → Application access

5. Auto-Start Containers on Reboot
I ensured the container automatically starts after a reboot by:
Using Docker’s restart policy (--restart unless-stopped or similar).
This guarantees:
If the EC2 instance restarts, the application container runs automatically without manual intervention.


6. Final Result
The application runs inside a Docker container on an AWS EC2 instance.
It is:
Cost-efficient
Portable
Automatically recoverable after reboot
