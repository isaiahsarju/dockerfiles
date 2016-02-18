# Start from base Ubuntu image
FROM ubuntu

#Prep programs needed
RUN apt-get -y install python
RUN apt-get -y install curl
RUN apt-get -y install git

#Install Pip
RUN curl https://bootstrap.pypa.io/get-pip.py > get-pip.py
RUN python get-pip.py

#Get InSpy.Py
RUN git clone https://github.com/gojhonny/InSpy.git
WORKDIR InSpy
RUN chmod +x InSpy.py
RUN pip install -r requirements.txt

#Start in bash prompt
CMD ["/bin/bash"]
