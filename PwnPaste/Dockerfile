# Start from base Ubuntu image
FROM ubuntu

#Prep programs needed
RUN apt-get -y install wget

#Install PwnPaste
RUN wget https://github.com/gojhonny/pwnpaste/releases/download/v1.0.0/pwnpaste1.0.0linux-amd64.tar.gz
RUN tar -xvzf pwnpaste1.0.0linux-amd64.tar.gz
RUN mv pwnpaste1.0.0linux-amd64/pwnpaste .

#Start in bash prompt
CMD ["/bin/bash"]