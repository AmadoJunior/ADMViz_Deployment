#
# Build
#
FROM maven:3.8.4-openjdk-17-slim AS build

RUN apt-get update && apt-get install -y git

ARG GITHUB_REPO_URL

RUN git clone ${GITHUB_REPO_URL} /app

COPY ./application.properties /app/src/main/resources/application.properties

WORKDIR /app

RUN mvn clean package -DskipTests

#
# Package
#
FROM openjdk:17-slim

WORKDIR /app

COPY --from=build /app/target/*.jar /app/app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app/app.jar"]