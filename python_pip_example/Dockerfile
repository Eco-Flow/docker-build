FROM --platform=linux/amd64 python:3.11.9-slim

ARG gffread_version='0.12.7'
ARG gffread_architecture='Linux_x86_64'

RUN apt-get update \
    && apt-get install -y procps wget build-essential software-properties-common libcurl4-openssl-dev libssl-dev libexpat1-dev libjpeg-dev zlib1g-dev bzip2 \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN pip3 install Pillow
