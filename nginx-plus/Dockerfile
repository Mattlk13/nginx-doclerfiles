FROM debian:wheezy

MAINTAINER Konstantin Pavlov "thresh@nginx.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y -q wget apt-transport-https lsb-release

# Download certificate and key from the customer portal https://cs.nginx.com
ADD nginx-repo.crt /etc/ssl/nginx/
ADD nginx-repo.key /etc/ssl/nginx/
RUN wget -q -O /etc/ssl/nginx/CA.crt https://cs.nginx.com/static/files/CA.crt

RUN wget -q -O - http://nginx.org/keys/nginx_signing.key | apt-key add -

RUN wget -q -O /etc/apt/apt.conf.d/90nginx https://cs.nginx.com/static/files/90nginx

RUN printf "deb https://plus-pkgs.nginx.com/debian `lsb_release -cs` nginx-plus\n" >/etc/apt/sources.list.d/nginx-plus.list

RUN apt-get update && apt-get install -y nginx-plus

# forward request logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log

# Provide specific nginx.conf, if needed
# ADD nginx.conf /etc/nginx

# Mount host machine catalog to the container
# VOLUME /srv/static-files /usr/share/nginx/html

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf", "-g", "daemon off; error_log /dev/stderr warn;"]
