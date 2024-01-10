FROM ubuntu:22.04

ARG datasets_version="v16.1.2"
ARG datasets_architecture="linux-amd64" # linux-arm64 

RUN apt-get update \
    && apt-get install -y wget procps unzip \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN wget "https://github.com/ncbi/datasets/releases/download/${datasets_version}/${datasets_architecture}.cli.package.zip" && \
    unzip "${datasets_architecture}.cli.package.zip" -d /usr/local/bin && \
    rm /"${datasets_architecture}.cli.package.zip"
