FROM jenkins/inbound-agent:latest
USER root

RUN apt-get update && \
    apt-get install -y docker.io docker-compose

VOLUME /var/run/docker.sock

RUN usermod -aG docker jenkins

USER jenkins
