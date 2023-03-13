#
# Build
#
FROM debian:10 AS build

RUN apt-get update && apt-get -y install maven

WORKDIR /opt/shipping

COPY pom.xml /opt/shipping/
RUN mvn dependency:resolve
COPY src /opt/shipping/src/
RUN mvn package

#
# Run
#
FROM openjdk:8-jdk

EXPOSE 8080

WORKDIR /opt/shipping
# COPY --from=fzf53242.live.dynatrace.com/linux/oneagent-codemodules:java / /
# ENV LD_PRELOAD /opt/dynatrace/oneagent/agent/lib64/liboneagentproc.so
# COPY agent /agent/
# COPY AppServerAgent /appagent/
# COPY dynatrace-oneagent-zos-java.jar /dyna/
# COPY dtconfig.json /dyna/
#COPY opentelemetry-javaagent.jar /open/
#"-javaagent:/agent/sixthsense-agent.jar",
#"-javaagent:/appagent/javaagent.jar"
#"-javaagent:/dyna/dynatrace-oneagent-zos-java.jar",
# COPY dd-java-agent.jar /
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql
COPY newrelic /newrelic/

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD [ "java", "-Xmn256m", "-Xmx768m","-javaagent:/newrelic/newrelic.jar","-jar", "shipping.jar" ]
# -javaagent:/path/to/dd-java-agent.jar \
#   -Ddd.logs.injection=true \
#   -Ddd.service=robotshop-shipping \
#   -Ddd.env=shipping \

# docker run -d -v /var/run/docker.sock:/var/run/docker.sock:ro \
#           -v /proc/:/host/proc/:ro \
#           -v /sys/fs/cgroup/:/host/sys/fs/cgroup:ro \
#           -p 8126:8126/tcp \
#           -e DD_API_KEY=f791b8e3d2d7c35fcf01598cef485591f0cea300 \
#           datadog/agent:latest