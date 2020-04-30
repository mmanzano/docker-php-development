FROM centos:7
EXPOSE 9000
WORKDIR /var/www/web

RUN \
    yum -y update wget yum-utils&& \
	yum -y install deltarpm && \
	yum -y install epel-release && \
	rpm --import http://rpms.famillecollet.com/RPM-GPG-KEY-remi && \
    rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable extras && \
	yum-config-manager --enable epel && \
	yum-config-manager --enable remi && \
	yum-config-manager --disable remi-php55 && \
	yum-config-manager --disable remi-php56 && \
	yum-config-manager --disable remi-php70 && \
    yum-config-manager --disable remi-php71 && \
    yum-config-manager --disable remi-php73 && \
    yum-config-manager --disable remi-php74 && \
    yum-config-manager --enable  remi-php73 && \
	yum -y install \
           php73-php-fpm \
           php73-php-json \
           php73-php-xml \
           php73-php-mysqli \
           php73-php-mbstring \
           php73-php-mysqlnd \
           php73-php-gd \
           php73-php-ldap \
           php73-php-mcrypt \
           php73-php-pecl-zip \
           php73-php-soap \
           php73-php-intl \
           php73-php \
           php73-php-pdo \
           php73-php-pecl-imagick \
           nano


RUN mkdir -p /var/log/php-fpm
RUN ln -s /opt/remi/php73/root/sbin/php-fpm /usr/sbin/php-fpm
RUN ln -s /usr/bin/php73 /usr/bin/php
RUN ln -sf /dev/stderr /var/log/php-fpm/error.log

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=. --filename=composer \
    && mv composer /usr/local/bin/

COPY docker/php/www.conf /etc/opt/remi/php73/php-fpm.d/www.conf
CMD ["php-fpm", "-F"]