FROM phusion/baseimage:0.9.16
MAINTAINER Simon Elsbrock <simon@iodev.org>

ENV LANG en_US.UTF-8

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
CMD ["/sbin/my_init"]

#RUN echo 'Acquire::http::Proxy "http://10.42.23.55:3142";' > /etc/apt/apt.conf.d/90-apt-cacher.conf

RUN \
    echo "APT::Install-Recommends \"true\";\nAPT::Install-Suggests \"false\";" > /etc/apt/apt.conf ;\
    echo "Europe/Berlin" > /etc/timezone && DEBIAN_FRONTEND=noninteractive dpkg-reconfigure tzdata ;\
    locale-gen en_US.UTF-8 en_DK.UTF-8 de_DE.UTF-8 ;\
    apt-get -q -y update ;\
    apt-get install -y git nodejs npm ruby ruby-dev make gcc ;\
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ;\
    update-alternatives --install /usr/bin/node node /usr/bin/nodejs 10 ;\
    gem install jekyll --no-rdoc --no-ri ;\
    mkdir -p /etc/my_init.d

RUN \
    adduser --disabled-password --gecos "" dev

ADD install-deps.sh /etc/my_init.d/install-deps.sh

EXPOSE 8000
