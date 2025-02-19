FROM eclipse-temurin:8-jre
WORKDIR /app
COPY build/libs/cordapp-example-0.1.jar app.jar
EXPOSE 50005
ENTRYPOINT ["java", "-jar", "app.jar"]
