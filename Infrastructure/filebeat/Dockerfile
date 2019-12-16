FROM debian:latest
RUN apt-get update \
         && apt-get install -y --no-install-recommends \
         net-tools \
         netcat \
         python-pip \
         rsync \
         virtualenv \
         libpcap-dev \
      && rm -rf /var/lib/apt/lists/*
RUN pip install --upgrade pip
RUN pip install --upgrade setuptools
FROM docker.elastic.co/beats/filebeat:6.8.0
COPY ${PWD}/config/filebeat.yml /usr/share/filebeat/filebeat.yml
USER root
RUN chown root:filebeat /usr/share/filebeat/filebeat.yml
USER filebeat


