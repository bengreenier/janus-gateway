# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.187.0/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG VARIANT="focal"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install curl g++-10 git libmicrohttpd-dev libjansson-dev libssl-dev libsofia-sip-ua-dev libglib2.0-dev libopus-dev libogg-dev libcurl4-openssl-dev liblua5.3-dev libconfig-dev pkg-config gengetopt libtool automake python3 python3-pip python3-setuptools python3-dev python3-wheel ninja-build libavcodec-dev
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 100 --slave /usr/bin/g++ g++ /usr/bin/g++-10 --slave /usr/bin/gcov gcov /usr/bin/gcov-10
RUN pip3 install meson

ENV LIBNICE_VERSION=0.1.18
ENV LIBSRTP_VERSION=v2.3.0

# Libnice
RUN mkdir /tmp/libnice
WORKDIR /tmp/libnice
RUN curl -sLf https://github.com/libnice/libnice/archive/${LIBNICE_VERSION}.tar.gz | tar -zx --strip-components=1
RUN meson --prefix=/usr build/
RUN ninja -C build install

# Libsrtp
RUN mkdir /tmp/libsrtp
WORKDIR /tmp/libsrtp
RUN curl -sLf https://github.com/cisco/libsrtp/archive/${LIBSRTP_VERSION}.tar.gz | tar -zx --strip-components=1
RUN ./configure --prefix=/usr --enable-openssl
RUN make shared_library
RUN make install

