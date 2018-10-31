# General Purpose PHP Developmemt Docker Container
# Builds a PHP Apache enviroment you can map your 
# source into.

FROM ubuntu:16.04

MAINTAINER David J. Lodwig <david.lodwig@davelodwig.co.uk>

#	--------------------------------------------------
#	:: DEPENDENCIES
#	-------------------------------------------------- 

RUN apt-get update -y && apt-get install -y apache2 && apt-get install -y php libapache2-mod-php php-mcrypt php-mbstring php-mysql php-gd php-xml && apt-get install php-xdebug && apt-get install -y git && apt-get install -y vim && apt-get -y clean


#	--------------------------------------------------
#	:: APACHE CONFIG
#	--------------------------------------------------

COPY application/build/php_errors.ini /etc/php/7.0/apache2/conf.d/
COPY application/build/php_upload.ini /etc/php/7.0/apache2/conf.d/
COPY application/build/php_xdebug.ini /etc/php/7.0/apache2/conf.d/
COPY application/build/000-default.conf /etc/apache2/sites-available/000-default.conf

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_PID_FILE $APACHE_RUN_DIR/apache2.pid
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

#	--------------------------------------------------
#	:: START APACHE
#	--------------------------------------------------

EXPOSE 80 9090

CMD ["/usr/sbin/apache2", "-D",  "FOREGROUND"]