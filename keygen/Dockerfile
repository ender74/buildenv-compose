FROM debian:jessie
MAINTAINER Heiko Hüter <heiko.hueter@ender74.de>

RUN apt-get update && apt-get install -y openssh-client && apt-get clean

RUN adduser --home /home/jenkins --disabled-password --gecos '' jenkins

RUN mkdir /var/keys \
    && ssh-keygen -t rsa -b 4096 -C "http://ender74.github.io" -f /var/keys/id_rsa -N ""

ADD *.sh /var/keys/

VOLUME ["/var/keys"]