# u need machine
# docker-machine create --driver virtualbox --virualbox-memory 2028 --virtualbox-cpu-count 2 Char
FROM alpine:latest
MAINTAINER kroselin

RUN apk update && \
	apk add wget openjdk8-jre bash

WORKDIR minecraft

RUN wget https://launcher.mojang.com/v1/objects/bb2b6b1aefcd70dfd1892149ac3a215f6c636b07/server.jar \
	&& echo 'eula=true' > eula.txt

EXPOSE 25565

CMD bash
# ENTRYPOINT java -Xmx1024M -Xms1024M -jar server.jar nogui
