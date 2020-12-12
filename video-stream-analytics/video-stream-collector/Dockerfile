FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/jolfr/scene-substitution.git

FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone /app/scene-substitution/video-stream-analytics/video-stream-collector /app
RUN mvn clean
RUN mvn clean install
COPY --from=clone /app/scene-substitution/input /app/input
CMD ["java", "-jar", "video-stream-collector-1.0.0.jar"]
