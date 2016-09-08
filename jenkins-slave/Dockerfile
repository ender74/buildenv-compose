FROM debian:jessie
MAINTAINER Heiko Hüter <heiko.hueter@ender74.de>

#install ssh daemon
RUN apt-get update && apt-get install -y openssh-server && apt-get clean
RUN mkdir /var/run/sshd
RUN adduser --disabled-password --gecos '' jenkins \
	&& echo "jenkins:jenkins" | chpasswd \
	&& mkdir /home/jenkins/.ssh \
	&& chmod 700 /home/jenkins/.ssh \
	&& chown -R jenkins:nogroup /home/jenkins/.ssh

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

VOLUME ["/etc/ssh"]
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

RUN mkdir /var/keys
VOLUME ["/var/keys"]

#install java & maven
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list \
    && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 \
    && apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq oracle-java8-installer
RUN apt-get install -y maven

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV PATH $PATH:$JAVA_HOME/bin