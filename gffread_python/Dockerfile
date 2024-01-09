FROM python:3.10-slim

ARG gffread_version='0.12.7'
ARG gffread_architecture='Linux_x86_64'

RUN apt-get update \
    && apt-get install -y procps wget \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN wget "https://github.com/gpertea/gffread/releases/download/v${gffread_version}/gffread-${gffread_version}.${gffread_architecture}.tar.gz" && \
    tar -xf "gffread-${gffread_version}.${gffread_architecture}.tar.gz" -C /opt #Not a gzipped file despite extension && \
    chmod u+x "/opt/gffread-${gffread_version}.${gffread_architecture}/gffread" && \
    rm "/gffread-${gffread_version}.${gffread_architecture}.tar.gz"

ENV PATH="${PATH}:/opt/gffread-${gffread_version}.${gffread_architecture}"
