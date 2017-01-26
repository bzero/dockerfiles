FROM ubuntu
MAINTAINER Clebson Derivan <cderivan@gmail.com>
LABEL Description="Provide a fusion building environment ubuntu based"

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential wget libbz2-dev \
	qt5-qmake qt5-default libgtk2.0-dev libpq-dev g++ libgtop2-dev liblog4cpp5-dev \
	libcppunit-dev libxerces-c-dev libxml2-dev libxslt1-dev libjpeg-dev libgsoap-dev \
	cmake libsqlite3-dev libmysql++-dev unixodbc-dev apache2 apache2-dev  gsoap sqlite3 \
	uncrustify clang-format-3.6 astyle libaio-dev libudev-dev  libbz2-dev libpci-dev \
	libpciaccess-dev libkmod-dev libusb-dev meld pgadmin3 sqlitebrowser remmina remmina-plugin-rdp \
	remmina-plugin-vnc glogg libqt5webkit5-dev \
 	&& rm -rf /var/lib/apt/lists/*

ARG boost_version=1.59.0
ARG boost_dir=boost_1_59_0
ENV boost_version ${boost_version}

RUN wget http://downloads.sourceforge.net/project/boost/boost/${boost_version}/${boost_dir}.tar.gz \
    && tar xfz ${boost_dir}.tar.gz \
    && rm ${boost_dir}.tar.gz \
    && cd ${boost_dir} \
    && ./bootstrap.sh \
    && ./b2 --without-python --prefix=/usr -j 4 link=shared runtime-link=shared install \
    && cd .. && rm -rf ${boost_dir} && ldconfig


ARG soci_dir=soci-3.2.3
ENV soci_dir ${soci_dir}

RUN wget https://downloads.sourceforge.net/project/soci/soci/${soci_dir}/${soci_dir}.tar.gz \
    && tar xfz ${soci_dir}.tar.gz \
    && cd ${soci_dir} \
    && cmake -G "Unix Makefiles" \
    && make \
    && make install \
    && cd / && rm -rf /codes && ldconfig

ENV ORACLE_HOME /usr/include
CMD bash
