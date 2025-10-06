FROM maven:3.8.5-openjdk-17 AS build
COPY . .
RUN mvnw clean package -DskipTests 

FROM openjdk:17-jdk-slim
COPY --from=builder /app/target/lakeSide-hotel-demo-server-master.jar
EXPOSE 8080 
ENTRYPOINT ["java", "-jar", "app.jar"]