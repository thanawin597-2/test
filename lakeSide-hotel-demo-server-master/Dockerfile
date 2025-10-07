FROM maven:3.8.5-openjdk-17 AS build
COPY . /app
WORKDIR /app
RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-slim
COPY --from=build /app/target/lakeSide-hotel-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 9192
ENTRYPOINT ["java", "-jar", "app.jar"]


