FROM ubuntu:xenial
MAINTAINER tobias@neontribe.co.uk

WORKDIR /opt/

RUN apt-get update && apt-get upgrade -y
RUN apt-get -y install git vim htop nginx wget sudo software-properties-common python-software-properties gcc-5 g++-5 build-essential nodejs-legacy nodejs npm
RUN git clone https://github.com/devinit/D-Portal

WORKDIR /opt/D-Portal/bin
# RUN add-apt-repository -y ppa:chris-lea/node.js && apt-get -y update && apt-get -y install nodejs

WORKDIR /opt/D-Portal
RUN ./bin/npm_install

COPY dportal.ngnix.conf /etc/nginx/sites-available/default
COPY dportal.startup.sh /usr/local/bin/startup.sh

WORKDIR /opt/D-Portal/dstore
RUN ./dstore init

WORKDIR /opt/D-Portal/bin
RUN ./dstore_import_bd_ug_hn

# WORKDIR /opt/D-Portal/bin
# RUN ./dstore import activity_data.xml
COPY update.sh /usr/local/bin/update.sh
RUN chmod 777 /usr/local/bin/update.sh

WORKDIR /opt/D-Portal

EXPOSE 8011
EXPOSE 1408

ENTRYPOINT ["/usr/local/bin/startup.sh"]
# ENTRYPOINT ["/bin/bash"]

# vim: set filetype=dockerfile expandtab tabstop=2 shiftwidth=2 autoindent smartindent:
