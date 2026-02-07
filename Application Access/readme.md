Application Access – Explanation
After deploying the application on AWS EC2, the next step was to make it accessible to users over the internet.
Access Methods
The application can be accessed using either:
Elastic IP
A static public IP provided by AWS.
Even if the EC2 instance is stopped or restarted, the IP address remains the same.
Best choice for production environments.
OR
EC2 Public IP
Automatically assigned public IP when the instance is running.
Changes if the instance is stopped and started again.
Suitable for testing or short-term use.
Web Server Setup (NGINX)
To handle incoming requests, I installed and configured NGINX on the EC2 instance:
Updated the system packages to ensure stability.
Installed NGINX as a web server.
Started the NGINX service.
Enabled NGINX to start automatically on system reboot.
Verified that NGINX is running successfully.

NGINX acts as:
A web server Or a reverse proxy to forward requests to the Docker container running the application.
Final Access
The application can be accessed using:
Elastic IP + Port
or
EC2 Public IP + Port
Users can open the application directly in a browser using the assigned IP address.
Result
Application is publicly accessible.
Server services auto-start on reboot.
Deployment is stable and production-ready
