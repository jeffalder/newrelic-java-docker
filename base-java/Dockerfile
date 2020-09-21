FROM openjdk:11

RUN curl https://download.newrelic.com/newrelic/java-agent/newrelic-agent/current/newrelic-java.zip -o /tmp/newrelic-java.zip
WORKDIR /
RUN mkdir /newrelic && unzip /tmp/newrelic-java.zip && rm /tmp/newrelic-java.zip

# See https://docs.newrelic.com/docs/agents/java-agent/configuration/java-agent-configuration-config-file#cfg-log_file_name
ENV NEW_RELIC_LOG_FILE_NAME=STDOUT

# Using ENTRYPOINT here will prefix the CMD directive used in the app's Dockerfile.
# https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact
ENTRYPOINT ["java", "-javaagent:/newrelic/newrelic.jar"]