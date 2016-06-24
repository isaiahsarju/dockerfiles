# Instructions

## Build docker image
Edit Dockerfile as you like (as versions change)
	docker build -t lair2 .
## Create docker data container for data
	docker create -v /root/lair/db --name lairdata lair2 /bin/true
If you upgrade or wipe away lair2 image/container your data will still there as long as the folder stuctures stay the same (/root/lair/db)
## Run docker
**FIRST TIME** (or if you’ve rm'd the container):
	docker run --name lair -t -p 11013:11013 --volumes-from lairdata lair2
Should print out initial username/password after about 20 secs ^C and it will run in background (**wait until you see credentials for first time use**)
Docker control 
	docker ps -a
	docker stop lair
	docker start lair
Takes about 20 secs
## Interact with lair
Navigate to https://[DockerIP]:11013
**CHANGE PASSWORD if it’s your first time. You’ll never see it again.**
## When you’re done
	docker stop lair
To restart:
	docker start lair
