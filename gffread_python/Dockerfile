FROM --platform=linux/amd64 python:3.11.9-slim

ARG gffread_version='0.12.7'
ARG gffread_architecture='Linux_x86_64'

RUN apt-get update \
    && apt-get install -y procps wget perl bioperl bioperl-run build-essential software-properties-common libcurl4-openssl-dev libssl-dev libexpat1-dev zlib1g-dev bzip2 \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN wget "https://github.com/gpertea/gffread/releases/download/v${gffread_version}/gffread-${gffread_version}.${gffread_architecture}.tar.gz" && \
    tar -xf "gffread-${gffread_version}.${gffread_architecture}.tar.gz" -C /opt #Not a gzipped file despite extension && \
    chmod u+x "/opt/gffread-${gffread_version}.${gffread_architecture}/gffread" && \
    rm "/gffread-${gffread_version}.${gffread_architecture}.tar.gz"

ENV PATH="${PATH}:/opt/gffread-${gffread_version}.${gffread_architecture}"
