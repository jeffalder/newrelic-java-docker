FROM openjdk:11 AS builder
ADD . /app
WORKDIR /app
RUN ./gradlew bootJar

# Multi-stage builds: https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
FROM base-java
COPY --from=builder /app/build/libs/demo*jar /app/demo.jar
ENV NEW_RELIC_APP_NAME=docker-base-demo

EXPOSE 8080

# Using CMD here will suffix the ENTRYPOINT directive used in base-java's Dockerfile.
# https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact
CMD ["-jar", "/app/demo.jar"]