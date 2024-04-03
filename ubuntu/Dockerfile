FROM ubuntu:jammy-20240227

RUN apt-get update \
    && apt-get install -y procps \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*
