FROM jenkins
MAINTAINER Heiko Hüter <heiko.hueter@ender74.de>

USER root

ADD basic-security.groovy /usr/share/jenkins/ref/init.groovy.d/basic-security.groovy

RUN mkdir /var/keys
VOLUME ["/var/keys"]

USER ${user}

RUN /usr/local/bin/install-plugins.sh git