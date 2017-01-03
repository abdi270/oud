# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM oraclelinux:6.6

# Set correct environment variables.
ENV HOME /root

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.


# ...put your own build instructions here...

# Clean up APT when done.
#
## 
RUN yum install tar unzip -y &&  groupadd user && useradd -g user oracle  -m -d /app && mkdir -p /app/fmw /tmp/sw /app/oraInventory

WORKDIR  /tmp/sw

ADD oud-install.rsp oud-install.rsp
ADD oraInst.loc /app/oraInst.loc 

##
RUN curl -s -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u65-b17/jdk-8u65-linux-x64.tar.gz -o jdk.tgz &&  tar xfzC jdk.tgz /app
##
#
#RUN curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn/nt/middleware/11g/111220/ofm_oud_generic_11.1.2.2.0_disk1_1of1.zip   -o ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip

ADD oud.zip ofm_oud_generic_11.1.2.2.3_disk1_1of1.zip 

RUN unzip -q ofm_oud_generic_11.1.2.2.3_disk1_1of1.zip  &&  rm ofm_oud_generic_11.1.2.2.3_disk1_1of1.zip && chown -R oracle:user  /app
####
USER oracle
ENV JAVA_HOME /app/jdk1.8.0_65
ENV PATH $JAVA_HOME/bin:$PATH

WORKDIR   /tmp/sw/oud/Disk1

#
RUN ./runInstaller -debug -jreLoc $JAVA_HOME -silent -responseFile /tmp/sw/oud-install.rsp -invPtrLoc  /app/oraInst.loc -ignoreSysPrereqs -waitforcompletion -nocheckForUpdates -novalidation -noconsole 

#
#
# Use Oracle's init system.
USER root
CMD ["/sbin/init"]
