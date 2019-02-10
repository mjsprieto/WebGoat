FROM openjdk:11.0.1-jre-slim-stretch

ARG webgoat_version=v8.0.0.M23

RUN \
  apt-get update && apt-get install && \
  apt-get install authbind && \
  apt-get -y install sudo  && \
  useradd --home-dir /home/webgoat --create-home -U webgoat

USER webgoat
RUN cd /home/webgoat/; mkdir -p .webgoat-${webgoat_version}
COPY target/webgoat-server-${webgoat_version}.jar /home/webgoat/webgoat.jar

USER root

RUN touch /etc/authbind/byport/80
RUN chmod 777 /etc/authbind/byport/80

EXPOSE 80
EXPOSE 9001

ENTRYPOINT ["authbind", "--deep", "java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/home/webgoat/webgoat.jar"]
CMD ["--server.port=80", "--server.address=0.0.0.0"]
