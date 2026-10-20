# Lab 3: Creating a Docker Image for a Java Application

In this lab, I containerized a Java calculator application using two different approaches.

### Part 1: Build Inside Docker
- Used a Maven image with Java 17.
- Created a working directory and a non-root user.
- Built the application inside Docker using `mvn package`.
- Built the image as `app1` and tested the calculator.

Image size: 764 MB disk usage, 240 MB content size.

### Part 2: Build Locally
- Built the application locally using Maven.
- Used a Java 17 runtime image with a non-root user.
- Copied the generated JAR file into the image.
- Built the image as `app2` and verified the calculator output.

Image size: 423 MB disk usage, 110 MB content size.

### Bonus: Image Size Comparison

The second image was approximately smaller thhan  disk usage. This is because it uses a Java runtime image without including Maven and the build tools.

Both approaches successfully built and ran the calculator application.
