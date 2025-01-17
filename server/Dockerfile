FROM node:22.12.0-bookworm AS dev

WORKDIR /usr/src

COPY bin/configure-apt.sh ./

RUN ./configure-apt.sh && \
    apt-get update && \
    apt-get install --no-install-recommends -yqq \
    jq \
    wget \
    nginx \
    nmap \
    toilet \
    bash \
    figlet \
    curl \
    tini \
    && apt-get clean

FROM node:22.12.0-bookworm-slim AS prod

WORKDIR /usr/src

COPY bin/configure-apt.sh ./

RUN ./configure-apt.sh && \
    apt-get update && \
    apt-get install --no-install-recommends -yqq \
    jq \
    wget \
    nginx \
    nmap \
    toilet \
    bash \
    figlet \
    curl \
    tini \
    && apt-get clean
