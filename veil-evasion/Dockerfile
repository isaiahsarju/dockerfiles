#From kali base
FROM kalilinux/kali-linux-docker
WORKDIR /root
RUN apt-get update
RUN apt-get -y install veil-evasion
RUN echo 'y' | veil-evasion
CMD ["/bin/bash"]
