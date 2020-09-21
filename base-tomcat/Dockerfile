FROM tomcat:8.5-jdk11-adoptopenjdk-hotspot

RUN apt-get update && apt-get install unzip
RUN curl https://download.newrelic.com/newrelic/java-agent/newrelic-agent/current/newrelic-java.zip -o /tmp/newrelic-java.zip
WORKDIR /
RUN mkdir /newrelic && unzip /tmp/newrelic-java.zip && rm /tmp/newrelic-java.zip

# See https://docs.newrelic.com/docs/agents/java-agent/configuration/java-agent-configuration-config-file#cfg-log_file_name
ENV NEW_RELIC_LOG_FILE_NAME=STDOUT

ENV CATALINA_OPTS ${CATALINA_OPTS} -javaagent:/newrelic/newrelic.jar