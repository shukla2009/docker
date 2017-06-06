# build the image and run it as
#
# docker run -d opscenter
#
# then open in the browserÂ http://OPSCENTER_CONTAINER_IP_ADDRESS:8888

FROM nimmis/java:oracle-8-jdk

ARG USER
ARG PASS
ARG VERSION

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y install adduser \
    curl \
    lsb-base \
    procps \
    zlib1g \
    gzip \
    python \
    ntp bash tree && \
    rm -rf /var/lib/apt/lists/*

RUN wget http://launchpadlibrarian.net/109052632/python-support_1.0.15_all.deb
RUN dpkg -i python-support_1.0.15_all.deb

#RUN wget http://172.25.30.61:8000/opscenter-$VERSION.tar.gz
RUN wget --user $USER -password $PASS http://downloads.datastax.com/enterprise/opscenter-$VERSION.tar.gz
RUN tar -xvzf opscenter-$VERSION.tar.gz

RUN mv opscenter-$VERSION opscenter
RUN ls
#RUN cd opscenter-$VERSION



# Agent and web ui
EXPOSE 8888 50031 61620

#ENTRYPOINT ["/opt/opscenter/bin/opscenter"]

CMD ["opscenter/bin/opscenter","-f"]
#CMD ["bash"]
#CMD /bin/bash -c "while true;do env | sort && sleep ${SLEEP_SECONDS:-30};done"