FROM openjdk:8-jre-alpine

EXPOSE 8080

COPY ./target/my-java-app-1.0.jar /usr/app/
WORKDIR /usr/app

ENTRYPOINT ["java", "-jar", "target/my-java-app-1.0.jar"]