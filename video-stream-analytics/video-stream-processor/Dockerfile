FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/jolfr/scene-substitution.git

FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone /video-stream-analytics/video-stream-processor /app
RUN mvn clean package exec:java -Dexec.mainClass="com.iot.video.app.spark.processor.VideoStreamProcessor"

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/spring-petclinic-1.5.1.jar /app
CMD ["java -jar spring-petclinic-1.5.1.jar"]