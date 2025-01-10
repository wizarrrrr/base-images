FROM node:22.12.0-bookworm@sha256:0e910f435308c36ea60b4cfd7b80208044d77a074d16b768a81901ce938a62dc AS dev

WORKDIR /usr/src/app

COPY bin/configure-apt.sh ./

RUN ./configure-apt.sh && \
    apt-get update && \
    apt-get install --no-install-recommends -yqq \
        autoconf \
        build-essential \
        cmake \
        jq \
        wget

COPY bin/* ./

FROM node:22.12.0-bookworm-slim@sha256:35531c52ce27b6575d69755c73e65d4468dba93a25644eed56dc12879cae9213 AS prod

WORKDIR /build

COPY bin/configure-apt.sh bin/install-ffmpeg.sh  ./

RUN apt-get update && \
    apt-get install curl ca-certificates --no-install-recommends -yqq && \
    ./configure-apt.sh && \
    apt-get update && \
    apt-get install --no-install-recommends -yqq \
        jq \
        wget \
    ./install-ffmpeg.sh && \
    apt-get autoremove -yqq && \
    apt-get clean && \
    rm -rf \
        configure-apt.sh \
        install-ffmpeg.sh

COPY --from=dev /usr/local/lib/ /usr/local/lib/

WORKDIR /usr/src/app