FROM debian:jessie
MAINTAINER Heiko Hüter <heiko.hueter@ender74.de>

RUN apt-get update && apt-get install -y openssh-client && apt-get clean

RUN mkdir /keys \
    && chmod 755 /keys \
    && ssh-keygen -t rsa -b 4096 -C "http://ender74.github.io" -f /keys/id_rsa

VOLUME ["/keys"]