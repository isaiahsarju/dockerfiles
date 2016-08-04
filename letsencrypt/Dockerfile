# Based on https://github.com/letsencrypt/letsencrypt/blob/master/Dockerfile 02/09/2016
# Making own to prevent needing to clone then install
# This will allow you to make a let's encrypt docker w/o cloning first
# docker create -v /etc/letsencrypt -v /root/.config/letsencrypt --name letsencryptdata letsencrypt /bin/true
# docker run --volumes-from=letsencryptdata -it --name=letsencrypt letsencrypt

# From ubuntu base
FROM ubuntu
WORKDIR /root

# Get git
RUN apt-get update
RUN apt-get -y install wget

# Download letsencrypt files
RUN wget https://dl.eff.org/certbot-auto
RUN chmod a+x ./certbot-auto
RUN sed -i 's/apt-get install/apt-get -y install/g' certbot-auto
RUN ./certbot-auto --os-packages-only --no-self-upgrade

CMD ["/bin/bash"]
