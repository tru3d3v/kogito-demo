#FROM quay.io/keycloak/keycloak:latest as builder
#FROM debian:stable-slim as builder
#FROM redhat/ubi9-micro:9.4-6 as builder
FROM openjdk:22-jdk-bookworm as builder
#FROM redhat/ubi9-micro:9.4-6 as builder

#RUN  dpkg --add-architecture arm64 &&  apt-get update &&  apt-get -y install libc6:arm64


COPY entrypoint.sh /opt/console-management/entrypoint.sh 

RUN apt-get update && apt-get -y install curl && apt-get -y install unzip 
#RUN  curl -H "Accept: application/zip" https://repository.jboss.org/org/kie/kogito/management-console/1.5.0.Final/management-console-1.5.0.Final-runner.jar -o management-console-runner.jar
RUN  curl -H "Accept: application/zip" https://repository.jboss.org/org/kie/kogito/management-console/991.0.1-SNAPSHOT/management-console-991.0.1-20201203.163939-1-runner.jar -o management-console-runner.jar

#FROM quay.io/keycloak/keycloak:latest
#FROM debian:stable-slim
#FROM redhat/ubi9-micro:9.4-6
FROM openjdk:22-jdk-bookworm


COPY --from=builder management-console-runner.jar /opt/console-management/management-console-runner.jar
COPY --from=builder /opt/console-management/entrypoint.sh /opt/console-management/entrypoint.sh 

RUN chmod +x /opt/console-management/entrypoint.sh


#ENV JAVA_HOME /opt/jdk22
RUN echo $JAVA_HOME

# change these values to point to a running postgres instance
ENV KOGITO_DATAINDEX_HTTP_URL=<URL>
#ENTRYPOINT ["java", "-Dquarkus.http.port=8080" ,"-Dquarkus.http.cors=true","-Dkogito.dataindex.http.url",$KOGITO_DATAINDEX_HTTP_URL,"-jar","/opt/console-management/management-console-runner.jar"]
ENTRYPOINT ["/opt/console-management/entrypoint.sh"]