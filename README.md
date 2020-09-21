# Demo Container Images for the Java agent

This repo is intended for base image maintainers. You might be one if you update or manage images that one or more Java services build from. This repo has an example of how to configure two base images: one that is bare Java and another generates a war for Tomcat.

The Dockerfiles are broken out so that configuration that is general for all purposes goes in the base Dockerfile. This would include the New Relic agent version, the Java version, and the agent configuration files. The individual app Dockerfiles have their own configuration for the appName setting and command-line.

## What the directories are

`base-java`: a base image that is only Java, and is ready to run the application's jar with New Relic.

`base-tomcat`: a base image that has Tomcat 8.5 installed, ready to run with New Relic.

`demo-app`: an extremely simple hello-world app that responds on localhost:8080/hello. In Tomcat, the URL path is `/demo/hello` due to packaging.

## How to run Java-only

1. Build the two container images:
   ```
   docker build -t base-java base-java
   docker build -t demo-app demo-app
   ```
2. Run the container:
   ```
   docker run --rm -it -p 8080:8080 -e NEW_RELIC_LICENSE_KEY=<your APM license key> demo-app:latest
   ``` 
3. Test:
   ```
   curl localhost:8080/hello
   ```
   
## How to run Tomcat

1. Build the two container images:
   ```
   docker build -t base-tomcat base-tomcat
   docker build -t demo-app-tomcat -f demo-app/Dockerfile.tomcat demo-app
   ```
2. Run the container:
   ```
   docker run --rm -it -p 8080:8080 -e NEW_RELIC_LICENSE_KEY=<your APM license key> demo-app-tomcat:latest
   ```
3. Test (note this is different due to the WAR URL path):
   ```
   curl localhost:8080/demo/hello
   ``` 