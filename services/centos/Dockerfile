# only for source code reading

ARG CENTOS_VERSION
FROM ${CENTOS_VERSION}

RUN yum -y install httpd; yum clean all; systemctl enable httpd.service

RUN yum -y install gcc gcc-c++

RUN yum -y install git make redhat-rpm-config libxml2-devel pkgconfig openssl-devel bzip2-devel curl-devel libpng-devel libjpeg-devel libXpm-devel freetype-devel gmp-devel libmcrypt-devel mariadb-devel aspell-devel recode-devel autoconf bison re2c libicu-devel systemd-devel systemtap-sdt-devel

CMD ["/usr/sbin/init"]

WORKDIR /home/webroot/