# Docker Environment Variables & Resource Management Lab 🚀

Welcome to my submission for **Lab 6: Docker Environment Variables and Resource Management**.  
This repository contains the setup, Dockerfiles, and step-by-step commands used to build, containerize, and configure a Python application with custom environment variables and strict resource limits.

---

## 📌 Objectives
1. Build and containerize a Python Flask application using Docker.
2. Manage environment variables using multiple approaches:
   - Direct injection via CLI flags (`-e`).
   - Loading from external environment files (`--env-file`).
   - Hardcoding variables inside the `Dockerfile` (`ENV`).
3. Enforce CPU and Memory resource restrictions on containers.
4. Verify application responsiveness and environment configuration.

---

## 🛠️ Step-by-Step Implementation

### Step 1: Clone Repository
```bash
git clone [https://github.com/Ibrahim-Adel15/PythonApp.git](https://github.com/Ibrahim-Adel15/PythonApp.git)
cd PythonApp
```

Step 2: Containerization (container1 - CLI Environment Variables)
1. Dockerfile Creation
Created a lightweight Dockerfile based on python:3.12-slim:

Dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY . /app
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]
2. Build Image
Bash
docker build -t ivolve1 .
3. Run Container with Resource Limits & Environment Variables
Ran container1 mapped to host port 5004 (to avoid host port conflicts) with a limit of 1 CPU and 256MB RAM:

Bash
docker run -d --name container1   -p 5004:5000  -e APP_NAME=iVolveApp1 -e APP_ENV=stg --cpus="1.0" -m 256m ivolve1

<img src="./pic1">
<img src="./pic1.1">
