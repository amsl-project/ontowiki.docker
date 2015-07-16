FROM ubuntu:14.10

MAINTAINER Sebastian Nuck <nuck@ub.uni-leipzig.de>

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# update ubuntu trusty
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get update

# install some basic packages
# install the nginx server with PHP
# install virtuoso
RUN apt-get -f install -y --force-yes \ 
	git make curl wget locate nginx-light php5-fpm php5-odbc php5-curl \
	virtuoso-opensource

# config php.ini
RUN sed -i "/^max_execution_time/c\max_execution_time = 120" /etc/php5/fpm/php.ini
RUN sed -i "/^memory_limit/c\memory_limit = 512M" /etc/php5/fpm/php.ini
RUN sed -i "/^upload_max_filesize/c\upload_max_filesize = 128M" /etc/php5/fpm/php.ini
RUN sed -i "/^post_max_size/c\post_max_size = 256M" /etc/php5/fpm/php.ini
RUN sed -i "/^short_open_tag/c\short_open_tag = On" /etc/php5/fpm/php.ini

# configure the ontowiki site for nginx
ADD ontowiki.conf /etc/nginx/sites-available/
RUN rm /etc/nginx/sites-enabled/default
RUN ln -s /etc/nginx/sites-available/ontowiki.conf /etc/nginx/sites-enabled/

# configure odbc for virtuoso
ADD odbc.ini /etc/

# Add startscript and start
ADD start.sh /start.sh
ADD ow-docker.fig /ow-docker.fig
CMD ["/bin/bash", "/start.sh"]

# expose the HTTP port to the outer world
EXPOSE 80 8890
