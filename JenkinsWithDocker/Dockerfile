FROM jenkins/jenkins:latest-jdk21
USER root

RUN apt-get update && \
    apt-get install -y docker.io docker-compose

RUN usermod -aG docker jenkins
