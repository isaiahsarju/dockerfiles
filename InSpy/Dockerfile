# Start from base Ubuntu image
FROM ubuntu

#Prep programs needed
RUN apt-get -y install python
RUN apt-get -y install curl

#Install Pip
RUN curl https://bootstrap.pypa.io/get-pip.py > get-pip.py
RUN python get-pip.py

#Install deps
RUN pip install BeautifulSoup
RUN pip install requests==2.5.3

#Get InSpy.Py
RUN curl https://raw.githubusercontent.com/gojhonny/Pentesting-Scripts/master/InSpy.py > InSpy.py
RUN chmod +x InSpy.py

#Start in bash prompt
CMD ["/bin/bash"]