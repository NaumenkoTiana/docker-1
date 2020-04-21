FROM debian:latest
MAINTAINER kroselin

ENV TS3SERVER_LICENSE=accept

WORKDIR /home/teamspeak

EXPOSE 9987/udp 10011 30033

RUN apt-get update && apt-get upgrade -y && \
	apt-get install -y wget bzip2 && \
	wget https://files.teamspeak-services.com/releases/server/3.11.0/teamspeak3-server_linux_amd64-3.11.0.tar.bz2 && \
	tar -xvf teamspeak3-server_linux_amd64-3.11.0.tar.bz2

WORKDIR teamspeak3-server_linux_amd64

RUN touch .ts3server_license_accepted

CMD sh ts3server_minimal_runscript.sh start license_accepted=1
# CMD /bin/bash

# How to run image
# docker run -d --name ts1 -p 9987:9987/udp -p 10011:10011 -p 30033:30033 teamspeak:myapp
