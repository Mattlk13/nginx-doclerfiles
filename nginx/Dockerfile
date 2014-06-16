FROM debian:wheezy

MAINTAINER Konstantin Pavlov "thresh@nginx.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y -q wget lsb-release
RUN wget -q -O - http://nginx.org/keys/nginx_signing.key | apt-key add -
RUN echo "deb http://nginx.org/packages/mainline/debian/ `lsb_release -cs` nginx" >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y nginx

# forward request logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log

# Provide specific nginx.conf, if needed
# ADD nginx.conf /etc/nginx

# Mount host machine directory to the container
# VOLUME /srv/static-files /usr/share/nginx/html

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf", "-g", "daemon off; error_log /dev/stderr warn;"]
