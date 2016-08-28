FROM centos:latest
MAINTAINER Romano Kleinwächter

COPY etc /etc

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

RUN yum -y update
RUN yum -y install \
  php70w \
  php70w-opcache \
  php70w-cli \
  php70w-pecl-xdebug \
  php70w-pdo \
  php70w-pdo_mysql \
  php70w-xml \
  php70w-gd \
  php-phpunit-PHPUnit \
  httpd \
  net-tools
RUN yum -y install python-setuptools
RUN easy_install supervisor

# install symfony tool
RUN php -r "readfile('https://symfony.com/installer');" > /usr/local/bin/symfony

# install composer
RUN cd /tmp \
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --filename=composer --install-dir=/usr/local/bin \
  && unlink composer-setup.php

# change permissions
RUN chmod +x /usr/local/bin/symfony \
  && chmod +x /usr/local/bin/composer

EXPOSE 9000
CMD ["/usr/bin/supervisord"]
