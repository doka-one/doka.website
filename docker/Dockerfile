# BASE
FROM alpine

# RUN
RUN apk add nginx; \
    mkdir /etc/ssl/private; \
    echo "<h1>Hello world!</h1>" > /var/www/localhost/htdocs/index.html;

ADD $PWD/content/*  /var/www/localhost/htdocs/
ADD $PWD/content/artefacts/0.1.0/*  /var/www/localhost/htdocs/artefacts/0.1.0/
ADD $PWD/content/artefacts/0.2.0/*  /var/www/localhost/htdocs/artefacts/0.2.0/

# CONFIGURATIONS

# nginx configuration
ADD $PWD/config/nginx.conf /etc/nginx/nginx.conf

# keys and certs

ADD $PWD/config/*.key /etc/ssl/private/
ADD $PWD/config/*.crt /etc/ssl/certs/
WORKDIR /var/www/localhost/htdocs

# ENTRYPOINT

COPY $PWD/config/entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/bin/sh", "/usr/local/bin/entrypoint.sh"]

# EXPOSE PORTS

EXPOSE 80
EXPOSE 443

# RUN COMMAND
CMD ["/bin/sh", "-c", "nginx -g 'daemon off;'; nginx -s reload;"]
