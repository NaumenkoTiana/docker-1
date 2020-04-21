# For Gitlab project u need BIG container and machine. So you need to do big Char:
# docker-machine create --driver virtualbox --virtualbox-memory 4048 --virtualbox-cpu-count 2 Char

FROM ubuntu:16.04
MAINTAINER kroselin
EXPOSE 443 80 22

# To mute Gitlab Term
ENV TERM xterm

# Install necessary packages
 
RUN apt update && apt upgrade -y && apt-get install -y curl ca-certificates openssh-server tzdata \
# Pull gitlab pack for updates
	&& curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash \
# Install gitlab-ce
		&& apt install -y gitlab-ce \
# Make ssh keys
		&& openssl genrsa -out /etc/ssl/gitlab.key 2048 \
		&& openssl req -new -x509 -key /etc/ssl/gitlab.key -out /etc/ssl/gitlab.crt -days 90 -subj /CN=gitlab.kroselin.com \
		&& echo "letsencrypt['enable'] = false \n\
# url-address
		external_url \"https://gitlab.kroselin.com\" # Must use https protocol \n\
# Make ssl cerificate
		nginx['ssl_certificate'] = \"/etc/ssl/gitlab.crt\" \n\
		nginx['ssl_certificate_key'] = \"/etc/ssl/gitlab.key\" \n\
# Reassign ssh-port
		gitlab_rails['gitlab_shell_ssh_port'] = 5050" >> /etc/gitlab/gitlab.rb \
		&& echo "PORT 5050 \n\
		PasswordAuthentication no \n\
		PubkeyAuthentication yes" >> /etc/ssh/sshd_config
# grafana doesn't work on last version of Gitlab, so we dissable it
RUN sed -i "s/# grafana\['enable'\] = true/grafana['enable'] = false/g" /etc/gitlab/gitlab.rb
# more time to mute 502 mistake
RUN sed -i "s/unicorn\['worker_timeout'\] = 60/unicorn\['worker_timeout'\] = 300/g" /etc/gitlab/gitlab.rb

CMD service ssh start \
	&& /opt/gitlab/embedded/bin/runsvdir-start & \
	gitlab-ctl reconfigure && gitlab-ctl tail

# git clone -c http.sslverify=false https://192.168.99.116:8081/root/test.git
# git clone ssh://git@192.168.99.116:8082/root/test.git
