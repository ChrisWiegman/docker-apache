FROM ubuntu:latest
MAINTAINER cwiegman@ufl.edu

EXPOSE 80 443

RUN echo 'Acquire::http::Pipeline-Depth "0";' > /etc/apt/apt.conf.d/00-pipeline
RUN apt-get -o Debug::Acquire::http=true update
RUN apt -y clean 
RUN apt -y update
RUN apt-get -y upgrade
RUN apt-get -y install \
    apache2 \
    iproute2

RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod env
RUN a2enmod dir
RUN a2enmod proxy
RUN a2enmod proxy_fcgi
RUN a2enmod headers
RUN a2enmod alias
RUN a2enmod cache
RUN a2enmod cgid
RUN a2enmod expires
RUN a2enmod suexec
RUN a2enmod unique_id

RUN echo "ServerName $(ip route get 8.8.8.8 | awk '{print $NF; exit}')" >> /etc/apache2/apache2.conf

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ADD vhost.conf /etc/apache2/sites-enabled/000-default.conf
ADD certs /etc/apache2/ssl/

RUN apt-get remove -y build-essential libz-dev iproute2
RUN apt-get autoremove -y
RUN apt-get clean

CMD /usr/sbin/apache2ctl -D FOREGROUND