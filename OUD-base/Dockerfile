FROM oracle/oraclelinux:6.6
MAINTAINER Abdi M. 

# Set correct environment variables.
# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
# ...put your own build instructions here...

# Clean up APT when done.
#
## 
RUN yum update && yum install tar unzip -y &&  groupadd user && useradd -g user oracle  -m -d /oracle 

USER oracle
RUN mkdir -p /oracle/kit/silent /oracle/oraInventory
ADD oud-install.rsp /oracle/kit/silent
ADD oraInst.loc /oracle

##
RUN curl -s -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u65-b17/jdk-8u65-linux-x64.tar.gz | tar xfzC - /oracle 

ENV JAVA_HOME /oracle/jdk1.8.0_65

#

#RUN curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn/nt/middleware/11g/111230/ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip   -o ofm_oud_generic_11.1.2.3.0_disk1_1of1.zip

#RUN unzip -q ofm_oud_generic_11.1.2.2.3_disk1_1of1.zip  &&  rm ofm_oud_generic_11.1.2.2.3_disk1_1of1.zip && chown -R oracle:user  /oracle
####

#
#RUN ./runInstaller -debug -jreLoc $JAVA_HOME -silent -responseFile /tmp/sw/oud-install.rsp -invPtrLoc  /oracle/oraInst.loc -ignoreSysPrereqs -waitforcompletion -nocheckForUpdates -novalidation -noconsole 
#
#
#
# Use Oracle's init system.
USER oracle
CMD ["bash"]
