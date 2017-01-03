# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM oud-base

# Set correct environment variables.
USER oracle 
ENV ROOT /app/fmw
ENV PWF /app/.pwd
ENV ORACLE_HOME $ROOT/OUD
ENV OUDBIN $ORACLE_HOME/bin
### Server1 
ENV HOST1 localhost
ENV LDAPPORT1 10389
ENV LDAPSPORT1 10636
ENV ADMINPORT1 10444
ENV REPLPORT1 10989
###
ENV BASEDN dc=example,dc=com
ENV ROOTUSER cn=dirman

ENV INSTANCE_NAME oud1

WORKDIR $ORACLE_HOME
RUN echo Oracle123 > $PWF  ;  ./oud-setup  --cli  --baseDN "$BASEDN"  --addBaseEntry  --ldapPort $LDAPPORT1  --ldapsPort $LDAPSPORT1  --generateSelfSignedCertificate  --enableStartTLS  --adminConnectorPort $ADMINPORT1  --rootUserDN "$ROOTUSER"  --rootUserPasswordFile $PWF  --hostName $HOST1  --no-prompt  --noPropertiesFile

ENTRYPOINT  ["/app/fmw/oud1/OUD/bin/start-ds" , "--nodetach"]
