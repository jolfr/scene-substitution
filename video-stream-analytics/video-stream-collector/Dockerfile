FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/jolfr/scene-substitution.git

FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone /app/scene-substitution/video-stream-analytics/video-stream-collector /app
RUN mvn clean package

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/video-stream-collector-1.0.0.jar /app
CMD ["java -jar video-stream-collector-1.0.0.jar"]