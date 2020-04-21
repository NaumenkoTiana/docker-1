FROM ruby:2.6.2
MAINTAINER kroselin

RUN apt-get update -y && apt-get install -y \
		build-essential \
		libpq-dev \
		sqlite3 \
		gem \
		curl
RUN gem install bundler:1.17.2
RUN gem install rails --no-document
RUN gem install rake -v 13.0.1 --no-document
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
        && apt-get install -y nodejs

ONBUILD COPY app/ /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD EXPOSE 3000
ONBUILD RUN bundle install
ONBUILD RUN rake _13.0.1_ db:migrate
ONBUILD RUN rake _13.0.1_ db:seed
#ONBUILD RUN rake _13.0.1_
