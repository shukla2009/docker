FROM nimmis/java:oracle-8-jdk


ARG USER
ARG PASS
ARG VERSION

RUN apt-get update && apt-get install -y apt-transport-https
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y install adduser \
    curl \
    lsb-base \
    procps \
    zlib1g \
    gzip \
    python \
    openssh-server \
    sysstat \
    ntp bash tree && \
    rm -rf /var/lib/apt/lists/*

RUN wget http://launchpadlibrarian.net/109052632/python-support_1.0.15_all.deb
RUN dpkg -i python-support_1.0.15_all.deb

RUN echo "deb https://$USER:$PASS@debian.datastax.com/enterprise stable main" | tee -a /etc/apt/sources.list.d/datastax.sources.list
RUN curl -L https://debian.datastax.com/debian/repo_key | apt-key add -

RUN apt-get update


RUN apt-get install -y dse-full
RUN apt-get install sudo
RUN apt-get install datastax-agent

RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]