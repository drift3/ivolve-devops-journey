# Part 2: Build Locally

In this part, I built the Java calculator locally using Maven, then packaged it in a lightweight Java 17 runtime image.

### What I did
- Built the application locally using `mvn clean package`.
- Created a Dockerfile using a Java 17 runtime image.
- Set up a working directory and a non-root user.
- Copied the generated JAR file into the image.
- Created the Docker image named `app2`.
- Ran the calculator and verified the results.

Image size: 423 MB disk usage, 110 MB content size.

The application ran successfully using the generated JAR file.
