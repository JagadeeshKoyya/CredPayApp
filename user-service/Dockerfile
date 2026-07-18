#stage:build
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B

#Copy the rest of the application code to the working directory
COPY src ./src
RUN mvn clean package -DskipTests

#stage:Run the application
FROM eclipse-temurin:22-jre-alpine
#create a non-root user to run the application
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

#Drop privileges to the non-root user
USER appuser
#Expose port 8080 to the outside world
EXPOSE 8080
#Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]