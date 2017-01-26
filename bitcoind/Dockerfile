FROM alpine:3.4

MAINTAINER Clebson Derivan <cderivan@gmail.com>

ENV BITCOIN_DATA=/bitcoin

RUN apk --no-cache --virtual build-dependendencies add autoconf \
	    automake \
	    boost-dev \
	    build-base \
	    openssl \
	    openssl-dev \
	    libtool \
	    db-dev \
	    file \
	    libevent-dev \
	    su-exec

ARG bitcoin_version=0.13.2
ARG bitcoin_dir=bitcoin-0.13.2
ENV bitcoin_version ${bitcoin_version}

RUN wget https://github.com/bitcoin/bitcoin/archive/v${bitcoin_version}.tar.gz  \
	&& tar xfz v${bitcoin_version}.tar.gz \
	&& rm v${bitcoin_version}.tar.gz \
	&& cd ${bitcoin_dir} \
	&& ./autogen.sh \
	&& ./configure \
	    --disable-tests \
	    --disable-bench \
	    --disable-ccache \
	    --with-gui=no \
	    --with-utils \
	    --with-libs \
	    --with-daemon \
	    --with-incompatible-bdb \
	&& make \
	&& make install \
	&& cd .. && rm -rf ${bitcoin_dir} 

RUN adduser -S bitcoin

VOLUME ["/bitcoin"]

COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 8332 8333 18332 18333 18444

CMD ["bitcoind"]

