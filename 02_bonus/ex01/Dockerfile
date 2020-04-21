FROM alpine:latest
MAINTAINER kroselin

RUN apk update && \
	apk add --virtual build-dependencies \
	build-base \
	gcc \
	wget \
	git \
	vim \
	bash

CMD bash
