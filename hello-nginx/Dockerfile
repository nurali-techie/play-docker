FROM docker.io/nginx
RUN apt-get update
RUN apt-get install -y vim curl

RUN rm -rf /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/nginx.conf

RUN mkdir /var/cache/nginx/m2cache
RUN chmod 777 /var/cache/nginx/m2cache

COPY nginx.conf /etc/nginx/
COPY images /usr/share/nginx/html/images/
