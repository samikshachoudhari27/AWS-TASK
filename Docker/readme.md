1. Create Dockerfile(s)
What it is: A Dockerfile is a text file that contains instructions on how to build a Docker image (a blueprint for your container).
Why it’s needed: It ensures that your app always runs in the same environment with all necessary dependencies installed.
Example steps inside a Dockerfile:
Choose a base image (like python:3.11 for Python apps).
Copy your app code into the image.
Install required libraries or dependencies.
Set environment variables if needed.
Define the command to run your app.

2. Run App Using Docker Containers
What it is: A container is a running instance of a Docker image.
Why it’s needed: Running the app inside a container isolates it from the host system. This prevents conflicts between different apps or versions.

How it works:
Build the Docker image using the Dockerfile:
docker build -t myapp:latest .
Run a container from that image:
docker run -d --name myapp-container myapp:latest
-d runs the container in detached mode (in the background).
--name gives the container a friendly name for easy management.

3. Expose Required Ports
What it is: Exposing ports allows your app inside the container to communicate with the outside world (e.g., your browser, other services).
Why it’s needed: Without exposing ports, your app will run inside the container but won’t be accessible from outside.
How it works:
docker run -d -p 8080:80 myapp:latest
-p 8080:80 maps port 80 inside the container (where the app runs) to port 8080 on your host.
You can now access the app at http://localhost:8080.

4. Ensure Containers Auto-Start on Reboot
What it is: Docker containers can be configured to restart automatically if the system restarts or if the container crashes.
Why it’s needed: Ensures your application is always running, which is crucial for production environments.
How it works:
docker run -d --restart always -p 8080:80 myapp:latest
--restart always ensures the container starts automatically after a reboot.

Other options:
unless-stopped: Restart unless the container was manually stopped.
on-failure: Restart only if the container exits with an error.
