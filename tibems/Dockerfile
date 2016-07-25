FROM tutum/centos

# Dont forget to ./warehouse.py /dir/to/installers
# 172.17.0.1 is my host address.  I don't know of a nice way of autodetecting this :(
#ENV warehouse_host http://172.17.0.1:18000

RUN useradd -ms /bin/bash tibco
ENV HOME /home/node

RUN yum -y install unzip wget

RUN mkdir -p /tmp/software && \
    cd /tmp/software
    #wget --quiet $warehouse_host/jdk-7u79-linux-x64.rpm && \
COPY jdk-8u92-linux-x64.rpm /tmp/software
RUN cd /tmp/software &&\
    rpm -Uvh jdk-8u92-linux-x64.rpm && \
    rm -rf /tmp/software

RUN mkdir -p /tmp/software && \
    cd /tmp/software
    #wget --quiet $warehouse_host/TIB_ems_8.2.1_linux_x86.zip && \
COPY TIB_ems-dev_8.3.0_linux_x86.zip /tmp/software
RUN cd /tmp/software && \
    unzip TIB_ems-dev_8.3.0_linux_x86.zip -d ems && \
    cd ems && \
    ./TIBCOUniversalInstaller-lnx-x86.bin -silent && \
    cd / && \
    rm -rf /tmp/software

EXPOSE 7222

COPY files/ems.sh /opt/tibco/ems/

RUN chmod +x /opt/tibco/ems/ems.sh && \
    chown -R tibco:tibco /opt/tibco/ && \
    chown -R tibco:tibco /home/user/tibco/

VOLUME /home/user/tibco/tibco/cfgmgmt/ems/data:rw

USER tibco
CMD /opt/tibco/ems/ems.sh
