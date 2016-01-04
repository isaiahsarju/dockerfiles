# Start from base Ubuntu image
FROM ubuntu

# Prep starting space
RUN apt-get update
RUN apt-get -y install curl
RUN apt-get -y install wget

# Install MongoDB
WORKDIR /root/lair
RUN mkdir /root/lair/db
RUN curl -o /root/lair/mongodb.tgz https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1404-3.0.6.tgz
RUN tar -zxvf mongodb.tgz

# Install Lair App
WORKDIR /root/lair
RUN wget https://github.com/lair-framework/lair/releases/download/v2.0.3/lair-v2.0.3-linux-amd64.tar.gz
RUN tar -zxvf lair-v2.0.3-linux-amd64.tar.gz
WORKDIR /root/lair/bundle
RUN /bin/bash -c 'curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.26.1/install.sh | bash \
	&& source /root/.bashrc \
	&& source /root/.nvm/nvm.sh \
	&& nvm install v0.10.40 \
	&& nvm use v0.10.40 \
	&& cd /root/lair/bundle/programs/server \
	&& npm install'

# Install Lair API
WORKDIR /root/lair
RUN wget https://github.com/lair-framework/api-server/releases/download/v1.1.0/api-server_linux_amd64
RUN chmod +x api-server_linux_amd64

# Caddy Reverse Proxy
WORKDIR /root/lair
RUN curl -o caddy.tar.gz 'https://caddyserver.com/download/build?os=linux&arch=amd64&features='
RUN tar -zxvf caddy.tar.gz
RUN openssl req -days 3650 -new -x509 -newkey rsa:2048 -nodes -keyout key.pem -out cert.pem -days 9999 -subj "/C=US/ST=LAIR/L=Lairville/O=Dis/CN=www.lair.fun"
RUN printf '0.0.0.0:11013\ntls cert.pem key.pem\nproxy /api localhost:11015\nproxy / localhost:11014 {\n  websocket\n}\n' > Caddyfile

# Create start.sh
WORKDIR /root/lair
RUN printf 'rm db/mongod.lock\n./mongodb-linux-x86_64-ubuntu1404-3.0.6/bin/mongod --dbpath=/root/lair/db --bind_ip=localhost --quiet --nounixsocket --replSet rs0 1>&- 2>&- &\nsleep 15s\nexport ROOT_URL=http://localhost\nexport PORT=11014\nexport MONGO_URL=mongodb://localhost:27017/lair\nexport MONGO_OPLOG_URL=mongodb://localhost:27017/local\nsource /root/.bashrc\nsource /root/.nvm/nvm.sh\nnvm use v0.10.40\n./mongodb-linux-x86_64-ubuntu1404-3.0.6/bin/mongo --eval '\''rs.initiate({_id:"rs0", members: [{_id: 1, host: "localhost:27017"}]})'\'' admin 1>&- 2>&-\nsleep 3s\ncd bundle\nnode main.js&\ncd ..\nexport API_LISTENER=localhost:11015\n./api-server_linux_amd64&\n./caddy --conf=Caddyfile&\nwhile true; do sleep 1000; done\n' > start.sh
RUN chmod +x start.sh
CMD ["/bin/bash","-c","/root/lair/start.sh"]
