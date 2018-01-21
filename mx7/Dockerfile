FROM debian:jessie
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
     && apt-get -y upgrade \ 
     && apt-get -y install git apache2 mysql-server-5.5
RUN { \
        echo debconf debconf/frontend select Noninteractive; \
        echo mysql-community-server mysql-community-server/root-pass \
            password ''; \
        echo mysql-community-server mysql-community-server/re-root-pass \
            password ''; \
        echo mysql-community-server mysql-community-server/remove-test-db select false; \
    } | debconf-set-selections \
    && apt-get update && apt-get install -y mysql-server
#RUN useradd -G www-data -d /home/admin admin
#USER admin
EXPOSE 80
VOLUME ["/etc/mysql", "/var/lib/mysql"]
CMD service mysql start
CMD apachectl -D FOREGROUND