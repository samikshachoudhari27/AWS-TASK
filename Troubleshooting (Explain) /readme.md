Troubleshooting – Explanation
1. App Not Accessible
Possible Causes:
Security Group does not allow inbound traffic on the application port.
Application is not running inside the container.
Wrong IP address or port used to access the app.
EC2 instance is stopped or unhealthy.

Troubleshooting Steps:
Check EC2 Security Group inbound rules (HTTP/HTTPS or custom port).
Verify the EC2 instance is running.
Confirm the correct EC2 Public IP / Elastic IP is used.
Check application logs to ensure the app started successfully.

Resolution:
Open the required port in the security group.
Restart the application or container if needed.

2. Container Running but Port Not Reachable
Possible Causes:
Port mapping is missing or incorrect.
Application inside the container is not listening on the expected port.
Docker container is bound to localhost instead of 0.0.0.0.

Troubleshooting Steps:
Verify Docker port mapping (host port → container port).
Check application configuration inside the container.
Confirm the app is listening on all network interfaces.

Resolution:
Correct the port mapping while running the container.
Update the application to listen on the correct port and IP.

3. ALB Health Check Failures
Possible Causes:
Health check path is incorrect.
Application is not responding on the health check endpoint.
Security Group blocks ALB traffic.
Application startup time is longer than health check timeout.

Troubleshooting Steps:
Verify health check path (e.g., / or /health).
Ensure the app returns HTTP 200 for health checks.
Check that EC2 Security Group allows traffic from ALB.
Review ALB target group health status.

Resolution:
Update health check path and port.
Increase health check timeout if needed.
Fix security group rules to allow ALB traffic.
