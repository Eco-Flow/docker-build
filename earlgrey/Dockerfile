FROM ubuntu:22.04

ARG datasets_version="v16.1.2"
ARG datasets_architecture="linux-amd64"

ARG earl_version="4.3.0"

RUN apt-get update \
    && apt-get install -y wget procps unzip bzip2 \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

RUN wget -v "https://anaconda.org/bioconda/earlgrey/${earl_version}/download/linux-64/earlgrey-${earl_version}-h4ac6f70_0.tar.bz2" -O earlgrey.tar.bz2 && \
    mkdir -p /opt/earlgrey && \
    tar -xjf earlgrey.tar.bz2 -C /opt/earlgrey && \
    rm earlgrey.tar.bz2

ENV PATH="${PATH}:/opt/earlgrey/bin"
