# Build stage
FROM gradle:8.14.3-jdk17-alpine AS build
WORKDIR /app

COPY . .

# FIX permission gradlew
RUN chmod +x ./gradlew

RUN ./gradlew clean build -x check -x test -Pproduction --no-daemon

# Run stage
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
