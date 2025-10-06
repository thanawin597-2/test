# Stage 1: ใช้สำหรับ Build JAR File (Build Image)
FROM openjdk:21-jdk-slim as builder

# กำหนด Working Directory ภายใน Docker
WORKDIR /app

# Copy ไฟล์ทั้งหมดที่จำเป็นสำหรับการ Build
COPY . .

# สั่ง Build โดยใช้ Maven Wrapper (mvnw)
# -DskipTests คือการข้ามการรัน Test เพื่อให้ Build เร็วขึ้น
RUN ./mvnw clean package -DskipTests

# --------------------------------------------------------------------------

# Stage 2: ใช้สำหรับรันแอปพลิเคชัน (Runtime Image)
# ใช้ JRE Image ที่เล็กกว่าเพื่อลดขนาด Container
FROM openjdk:21-jre-slim

# กำหนด Working Directory
WORKDIR /app

# Copy เฉพาะไฟล์ JAR ที่ Build สำเร็จแล้วจาก Stage แรกมา
COPY --from=builder /app/target/*.jar app.jar

# Command ที่ใช้รัน Service เมื่อ Container เริ่มต้น (คำสั่ง Start Command ของคุณ)
ENTRYPOINT ["java", "-jar", "app.jar"]