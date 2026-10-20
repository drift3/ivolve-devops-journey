FROM maven:3.9.6-eclipse-temurin-17

WORKDIR /app
RUN useradd -m normaluser
RUN chown -R normaluser:normaluser /app
COPY --chown=normaluser:normaluser . .
USER normaluser
RUN mvn package 
CMD ["java", "-jar", "target/calculator.jar"]
EXPOSE 8080


