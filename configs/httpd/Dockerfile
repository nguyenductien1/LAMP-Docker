FROM httpd:latest

# install vim, htop

RUN apt-get update -y \
    && apt-get install vim -y \
    && apt-get install htop \
    && mkdir -p /home/sites \
    && rm -rf /var/lib/apt/lists/*

# Copy data, configs image

COPY ./httpd.conf /usr/local/apache2/conf/httpd.conf
COPY ./httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf
#COPY ./certificates/cert.crt /home/sites/
#COPY ./certificates/pkey.key /home/sites/

# Open port 80, 443 on network container 

EXPOSE 80 443

CMD [ "httpd-foreground"]



