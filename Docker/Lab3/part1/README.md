# Part 1: Build Inside Docker

In this part, I built a Java calculator application inside Docker using Maven and Java 17.

### What I did
- Created a Dockerfile using a Maven image.
- Set up a working directory and a non-root user.
- Copied the source code and built the application using `mvn package`.
- Created the Docker image named `app1`.
- Ran the generated JAR file and verified the calculator output.

Image size: 764 MB disk usage, 240 MB content size.

The application ran successfully. The Dockerfile includes `EXPOSE 8080` as requested, although the provided calculator is a console application and does not serve HTTP traffic.
