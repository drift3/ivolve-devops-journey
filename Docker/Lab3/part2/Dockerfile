FROM eclipse-temurin:17-jre

WORKDIR /app

RUN useradd -m user1

COPY --chown=user1:user1 target/calculator.jar app.jar
USER user1

CMD ["java", "-jar", "app.jar"]
EXPOSE 8080
