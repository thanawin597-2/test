FROM marven:3-eclipse-timurin-17 AS build
COPY . .
RUN ./mvnw clean package -DskipTests 

FROM eclipse-temurin:17-alphine
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080 
ENTRYPOINT ["java", "-jar", "app.jar"]