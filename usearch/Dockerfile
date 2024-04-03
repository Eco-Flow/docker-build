FROM ubuntu:jammy-20240227

ARG usearch_version='11.0.667_i86linux32'

RUN apt-get update \
    && apt-get install -y procps wget \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN wget "https://www.drive5.com/downloads/usearch${usearch_version}.gz" -O /opt/usearch.gz && \
    gunzip /opt/usearch.gz && \
    chmod +x /opt/usearch

ENV PATH="${PATH}:/opt"
