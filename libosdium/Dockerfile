FROM alpine:latest
WORKDIR /libsodium
RUN apk -U upgrade \
 && apk add --no-cache make \
	 gcc \
	alpine-sdk \
 && wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz \
 && gunzip LATEST.tar.gz \
 && tar -xvf LATEST.tar \
 && cd libsodium-stable && ./configure \
 && make && make check \
 && make install

CMD ["/bin/sh"]
