FROM keopx/java

MAINTAINER keopx <keopx@keopx.net>

ENV DEBIAN_FRONTEND=noninteractive

# Set repositories
RUN \
   echo "deb http://ftp.de.debian.org/debian/ stretch main non-free contrib" > /etc/apt/sources.list && \
   echo "deb-src http://ftp.de.debian.org/debian/ stretch main non-free contrib" >> /etc/apt/sources.list && \
   echo "deb http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
   echo "deb-src http://security.debian.org/ stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
   apt-get -qq update && apt-get -qqy upgrade
   # Update repositories cache and distribution

RUN \
   apt-get -yqq install apt-transport-https ca-certificates python3-software-properties gnupg2

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
# 'me' User in the future.

# SOLR - https://github.com/dockerimages/docker-solr
ENV SOLR_VERSION 5.0.0
# ENV SOLR solr-$SOLR_VERSION - New
# OLD - http://archive.apache.org/dist/lucene/solr/3.6.2/apache-solr-3.6.2.tgz
ENV SOLR solr-$SOLR_VERSION
RUN \
   apt-get update && \
   apt-get -y install lsof curl procps && \
   mkdir -p /opt && \
   wget -nv --output-document=/opt/$SOLR.tgz http://archive.apache.org/dist/lucene/solr/$SOLR_VERSION/$SOLR.tgz && \
   tar -C /opt --extract --file /opt/$SOLR.tgz && \
   rm /opt/$SOLR.tgz && \
   ln -s /opt/$SOLR /opt/solr

# Clear.
RUN \
   apt-get clean && rm -rf /var/lib/apt/lists/*   
   
EXPOSE 8983
# We will Put Our Image dockerimages/systemd-solr over that you should directly build that if you plan to run this in production
CMD ["/bin/bash", "-c", "/opt/solr/bin/solr -f"]
