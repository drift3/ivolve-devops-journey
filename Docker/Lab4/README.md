# Lab 4: Docker Image Optimization & Export/Load

This lab demonstrates how to optimize a Docker image for a Java Spring Boot application using multi-stage builds, enforce non-root security practices, and export/import Docker images as TAR archives.

---

## 1. Initial Build & Execution (`image1`)

First, cloned the repository and built the initial Docker image using the default `Dockerfile`:

```bash

git clone [https://github.com/Ibrahim-Adel15/ImageOptimization-.git](https://github.com/Ibrahim-Adel15/ImageOptimization-.git)
cd ImageOptimization-
docker build -t image1 .
```

Ran a container named container1 from image1 on port 8081, verified it was working properly, then stopped and deleted it:

docker run -d --name container1 -p 8081:80 image1
docker stop container1
docker rm container1

<img src="./pic%201%20run%20the%20container%20the%20delete%20it.PNG">


2. Optimization using Multi-Stage Build & Non-Root Security
Created an optimized Dockerfile2 using a multi-stage build approach to reduce the image size and configure the application to run as a non-root user for security:

Dockerfile

<img src="./pic2">
# Stage 1: Build stage
FROM maven:3.9.15-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Runtime stage
FROM eclipse-temurin:17-jre-alpine

# Security: Create and use non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app

# Copy built artifact from stage 1
COPY --from=builder /app/target/demo-0.0.1-SNAPSHOT.jar app.jar
RUN chown appuser:appgroup app.jar

USER appuser

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
Built the optimized image as image2:

Bash
docker build -t image2 -f Dockerfile2 .
Image Size Comparison:
image1 (Initial): Larger size due to build tools and Maven dependencies left in the final image.

image2 (Optimized): Significantly smaller size because it only contains the JRE runtime and the executable .jar file.

3. Running container2 & Security Verification
Ran container2 from the optimized image image2, checked the active user inside the container to confirm non-root execution, then stopped and removed it:

Bash
docker run -d --name container2 -p 8081:80 image2
docker exec -it container2 whoami
docker stop container2
docker rm container2
The whoami command confirmed the container was running under a non-root user (user2 / appuser).

4. Exporting, Deleting, and Restoring Image (TAR)
Saved image2 as a TAR file named lab-image.tar, deleted image2 from the local host, and then restored it from the TAR archive:

Bash
# Save image to tar archive
docker save -o lab-image.tar image2

# Remove image from local Docker host
docker rmi image2

# Load image back from tar archive
docker load -i lab-image.tar
Verified that image2 was successfully restored to the local host and ready to use.
