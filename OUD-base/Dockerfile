# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM oracle/oraclelinux

# Set correct environment variables.
ENV HOME /root

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.


# ...put your own build instructions here...

# Clean up APT when done.
#
## 
RUN yum install tar -y
RUN yum install unzip -y
#
RUN groupadd user
RUN useradd -g user oracle  -m -d /app
##
#
RUN mkdir -p /app/fmw /app/sw /app/oraInventory
WORKDIR  /app/sw
##
RUN curl -s -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-x64.tar.gz -o jdk-7u72-linux-x64.tar.gz 
##
#RUN curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn/nt/middleware/11g/111220/ofm_oud_generic_11.1.2.2.0_disk1_1of1.zip   -o ofm_oud_generic_11.1.2.2.0_disk1_1of1.zip

ADD oud.zip /app/sw/ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip
RUN unzip ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip
#RUN rm ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip

WORKDIR  /app
RUN tar xf sw/jdk-7u72-linux-x64.tar.gz
#RUN rm sw/jdk-7u72-linux-x64.tar.gz

ADD oud-install.rsp /app/sw/oud-install.rsp
ADD oraInst.loc /app/oraInst.loc 

RUN chown -R oracle:user  /app
####
USER oracle
ENV JAVA_HOME /app/jdk1.7.0_72
ENV PATH $JAVA_HOME/bin:$PATH

WORKDIR   /app/sw/oud/Disk1
RUN cat /app/oraInst.loc
RUN echo $JAVA_HOME
RUN ls -l /app/oraInventory
RUN touch /app/oraInventory/foo
RUN ./runInstaller -jreLoc $JAVA_HOME -silent -responseFile /app/sw/oud-install.rsp -invPtrLoc  /app/oraInst.loc -ignoreSysPrereqs -waitforcompletion -nocheckForUpdates -novalidation -noconsole 
#RUN ./runInstaller -debug -jreLoc $JAVA_HOME -silent -responseFile /app/sw/oud-install.rsp -invPtrLoc  /app/oraInst.loc -ignoreSysPrereqs -waitforcompletion -nocheckForUpdates -novalidation -noconsole 

#
#
# Use Oracle's init system.
# USER root
# WORKDIR  /app
# RUN rm -rf /app/sw
# CMD ["/sbin/init"]
