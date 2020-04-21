FROM ubuntu:18.04
MAINTAINER kroselin

RUN apt-get update \
	&& apt-get install -y wget

WORKDIR minecraft

RUN wget -o ~/Minecraft.deb https://launcher.mojang.com/download/Minecraft.deb \
	&& apt install -y gdebi-core \
	&& gdebi -y ~/Minecraft.deb \
	&& dpkq -i Minecraft.deb 
CMD bash
