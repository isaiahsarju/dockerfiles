# Based on https://github.com/letsencrypt/letsencrypt/blob/master/Dockerfile 02/09/2016
# Making own to prevent needing to clone then install
# This will allow you to make a let's encrypt docker w/o cloning first
# docker create -v /etc/letsencrypt -v /root/.config/letsencrypt --name letsencryptdata letsencrypt /bin/true
# docker run --volumes-from=letsencryptdata -it --name=letsencrypt letsencrypt

# From ubuntu base
FROM ubuntu
WORKDIR /root

# Get git
RUN apt-get -y install git

# Download letsencrypt files
RUN git clone https://github.com/letsencrypt/letsencrypt

# Let's install let's encrypt
RUN mkdir /opt/letsencrypt

RUN mkdir -p /opt/letsencrypt/src/letsencrypt-auto-source/
RUN cp letsencrypt/letsencrypt-auto-source/letsencrypt-auto /opt/letsencrypt/src/letsencrypt-auto-source/letsencrypt-auto

WORKDIR /opt/letsencrypt
RUN /opt/letsencrypt/src/letsencrypt-auto-source/letsencrypt-auto --os-packages-only && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

WORKDIR /root

RUN mkdir -p /opt/letsencrypt/src/
RUN cp letsencrypt/setup.py /opt/letsencrypt/src/
RUN cp letsencrypt/README.rst /opt/letsencrypt/src/
RUN cp letsencrypt/CHANGES.rst /opt/letsencrypt/src/
RUN cp letsencrypt/MANIFEST.in /opt/letsencrypt/src/

#RUN mkdir -p /opt/letsencrypt/src/letsencrypt
RUN cp -r letsencrypt/letsencrypt /opt/letsencrypt/src/letsencrypt/

RUN cp -r letsencrypt/acme /opt/letsencrypt/src/acme

#RUN mkdir -p /opt/letsencrypt/src/letsencrypt-apache/
RUN cp -r letsencrypt/letsencrypt-apache /opt/letsencrypt/src/letsencrypt-apache

#RUN mkdir -p /opt/letsencrypt/src/letsencrypt-nginx/
RUN cp -r letsencrypt/letsencrypt-nginx /opt/letsencrypt/src/letsencrypt-nginx

WORKDIR /opt/letsencrypt
RUN virtualenv --no-site-packages -p python2 /opt/letsencrypt/venv && \
    /opt/letsencrypt/venv/bin/pip install \
    -e /opt/letsencrypt/src/acme \
    -e /opt/letsencrypt/src \
    -e /opt/letsencrypt/src/letsencrypt-apache \
    -e /opt/letsencrypt/src/letsencrypt-nginx

# Prep for running
ENV PATH /opt/letsencrypt/venv/bin:$PATH
#ENTRYPOINT [ "letsencrypt" ]
CMD ["/bin/bash"]
