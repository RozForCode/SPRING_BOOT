# FROM maven:3.6.3-openjdk-17-slim AS builder
# ARG VERSION=0.0.1-SNAPSHOT
# WORKDIR /build/
# COPY pom.xml /build/
# COPY src /build/src/

# RUN mvn clean package
# COPY target/booting-web-${VERSION}.jar target/application.jar

# FROM openjdk:11.0.8-jre-slim
# WORKDIR /app/

# COPY --from=builder /build/target/application.jar /app/
# CMD ["java", "-jar", "/path/to/application.jar"]

# Builder stage
FROM maven:3.6.3-openjdk-17-slim AS builder
ARG VERSION=0.0.1-SNAPSHOT
WORKDIR /build/
COPY pom.xml /build/
COPY src /build/src/

# Build the project with Maven, passing the VERSION argument
RUN mvn clean package -DVERSION=${VERSION}

# Runtime stage
FROM openjdk:17-jre-slim
WORKDIR /app/

# Copy the built JAR from the builder stage
COPY --from=builder /build/target/booting-web-${VERSION}.jar /app/application.jar

# Run the application
CMD ["java", "-jar", "/app/application.jar"]

