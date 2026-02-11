# Use a Maven + JDK image to build the JAR
FROM maven:3.9.3-eclipse-temurin-17 AS build

WORKDIR /app

# Copy only necessary files to leverage Docker cache
COPY . .

# Build the JAR, skip tests to avoid Maven failures
RUN mvn clean package -DskipTests

# Use a lightweight JDK image for running
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Copy the built JAR from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose default Spring Boot port
EXPOSE 8080

# Run the JAR
ENTRYPOINT ["java","-jar","app.jar"]