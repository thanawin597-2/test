FROM maven:3.8.5-openjdk-17 AS build
# 1. คัดลอกไฟล์ทั้งหมดไปยังโฟลเดอร์ /app ภายใน Docker Image
COPY . /app
# 2. ตั้งค่า Working Directory เป็น /app เพื่อให้ Maven หา pom.xml เจอ
WORKDIR /app
# 3. รัน Maven (ตอนนี้จะทำงานภายใน /app)
RUN mvn clean package -DskipTests 

FROM openjdk:17-jdk-slim
# 4. ต้องเปลี่ยนเส้นทาง Source Path เป็น /app/target/ 
COPY --from=build /app/target/lakeSide-hotel-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080 
ENTRYPOINT ["java", "-jar", "app.jar"]
