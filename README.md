# -Task-5-Docker-Security-Optimization-Enterprise-Scenario-

🎯 Objective

Optimize Docker images so they are secure, lightweight, efficient and ready for production deployment.

---

# Problem Statement 

The development team has built a Node.js application and everything works. Before releasing it to production, the Security Team reviews the Docker image and finds several issues:

•	❌ Image size is too large (slow deployments) 

•	❌ Container runs as root 

•	❌ Unnecessary packages are installed 

•	❌ Image contains security vulnerabilities 

•	❌ Production deployment is rejected 

---

# Analyze Our Current Docker Image

# Step 1: Open the Employee Service Folder

From your current terminal:

Navigate to the employee service 

Run: cd employee-service

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Employee%20service.png?raw=true)

---

# Step 2: Build the Existing Docker Image

Run: docker build -t employee-service:before .

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/build.png?raw=true)

---

# Step 3: Check the Image Size

Run: docker images

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/docker%20images.png?raw=true)

---

# Step 4: Inspect the Image Layers

Run: docker history employee-service:before

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/docker%20history.png?raw=true)

---

# Step 5: Check Which User Runs the Container

Run: docker run --rm employee-service:before whoami

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/whoami.png?raw=true)

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Baseline%20Report.png?raw=true)

---

# Docker Image Optimization

# Step 1: Use Alpine Linux, Replace: FROM node:22

with: FROM node:22-alpine

Update the Dockerfile and save the changes 

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Updated%20dockerfile%20.png?raw=true)

---

# Step 2: Create a .dockerignore

Create a file named: .dockerignore

inside employee-service.

Add:

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/dockerignore.png?raw=true)

---

# Step 3: Build the New Image

docker build -t employee-service:optimized .

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/optimized%20docker%20build.png?raw=true)

---

# Step 4: Check the Image Size

docker images

Compare:

employee-service:before

employee-service:optimized

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/optimized%20docker%20images.png?raw=true)

---

# Step 5: Check Image History

docker history employee-service:optimized

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/optimized%20docker%20history.png?raw=true)

Finally comparing the image sizes before and after 

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Before%20and%20After%20comparison%20.png?raw=true)

---

# Docker Security Hardening

The Security Team scans your Docker image and reports:

❌ Container runs as root

❌ Multiple vulnerabilities found

❌ Deployment blocked


# Step 1: Create a Dedicated User

Instead of running as root, we'll create our own user.

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

---

# Step 2: Change File Ownership

Our application files are currently owned by root.

We'll change that:

RUN chown -R appuser:appgroup /app

Now appuser owns the application files.

---

# Step 3: Switch to the Non-Root User

Finally:

USER appuser

Now every command after this point (including starting the application) runs as appuser instead of root.

---

# Step 4: Replace the Dockerfile with:

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/adduser.png?raw=true)

---

# Step 5: Build the Secure Image

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/build%20secure.png?raw=true)

---

# Step 6: Verify the User

Run: docker run --rm employee-service:secure whoami

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/secure%20docker%20images.png?raw=true)

---

# Step 7: Install Trivy using Winget

Open cmd run: winget install AquaSecurity.Trivy

After installation close cmd and open a new cmd window.

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Trivy%20Installed.png?raw=true)

---

# Step 8: Verify Trivy

trivy --version

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Trivy%20version%20.png?raw=true)

---

# Step 9: Scan docker image with Trivy and verify downloads its vulnerability database

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Trivy%20Scan.png?raw=true)

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Report%20Summary.png?raw=true)

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Report%20summary%20extension%20.png?raw=true)

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Vulnerabilities.png?raw=true)

![image alt](https://github.com/ajaykumargk2k9/-Task-5-Docker-Security-Optimization-Enterprise-Scenario-/blob/main/Vulnerabilities%20extension%20.png?raw=true)

---



