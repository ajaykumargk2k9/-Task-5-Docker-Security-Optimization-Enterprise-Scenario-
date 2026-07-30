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

