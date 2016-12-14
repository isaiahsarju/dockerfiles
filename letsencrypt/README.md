README
======

Based on https://github.com/letsencrypt/letsencrypt/blob/master/Dockerfile 02/09/2016
Making my own so I don't need to clone then install
This will allow you to make a let's encrypt docker w/o cloning first
I use this for manually installing certs on another host
Make sure to use a secure transport method to move cert from docker to actual web host.

Installation
------------
~~~
curl https://raw.githubusercontent.com/isaiahsarju/dockerfiles/master/letsencrypt/Dockerfile -o Dockerfile
docker build -t letsencrypt .
~~~~
To Run
~~~~
docker -it --name=letsencrypt letsencrypt
~~~~
Then run
~~~~
letsencrypt
~~~~
or
~~~~
certbot-auto
~~~~
