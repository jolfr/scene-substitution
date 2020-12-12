FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/jolfr/scene-substitution.git

FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone app/scene-substitution/video-stream-analytics/video-stream-processor /app
RUN mvn clean install

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/video-stream-processor-1.0.0.jar /app
RUN mkdir output
CMD ["java", "-jar", "video-stream-processor-1.0.0.jar"]
