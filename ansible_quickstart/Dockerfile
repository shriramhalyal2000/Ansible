# containerizinf the application

FROM node:18-alpine AS base

WORKDIR /app

COPY package*.json .

# clean install npm for dependency
RUN npm run ci

FROM node:18-alpine AS builder

WORKDIR /app

COPY . .

# building the app from code
RUN npm run build


FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/build .
COPY --from=builder /app/dist .

EXPOSE 80

CMD ["npm" "start"]

---

    # containreizingf the jave application

    FROM maven:3.9-eclipse-termurin-21 AS build
    WORKDIR /app
    COPY pom.xml
    COPY src /.src

    RUN mvn clean package -DskipTests


# Stage 2: Create the lightweight runtime image
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Create a non-root user for security
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# Copy the built JAR from the build stage
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
