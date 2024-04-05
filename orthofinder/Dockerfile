FROM --platform=linux/amd64 python:3.11.9-slim

ARG orthofinder_version='2.5.5'
ARG diamond_version='2.1.9'
ARG fastme_version='2.1.6.3'

RUN apt-get update \
    && apt-get install -y procps wget mcl automake gcc make ncbi-blast+ \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache numpy scipy

RUN wget "https://gite.lirmm.fr/atgc/FastME/-/archive/v${fastme_version}/FastME-v${fastme_version}.tar.gz" -O /opt/FastME.tar.gz && \
    tar xvzf /opt/FastME.tar.gz -C /opt && \
    cd "/opt/FastME-v${fastme_version}" && ./configure --disable-dependency-tracking && make && make install && \
    rm /opt/FastME.tar.gz 

RUN wget "https://github.com/davidemms/OrthoFinder/releases/download/${orthofinder_version}/OrthoFinder.tar.gz" -O /opt/OrthoFinder.tar.gz && \
    tar xvzf /opt/OrthoFinder.tar.gz -C /opt && \
    rm /opt/OrthoFinder.tar.gz 

RUN rm /opt/OrthoFinder/bin/* && \
    ln -s /usr/bin/mcl /opt/OrthoFinder/bin/mcl && \
    ln -s /usr/local/bin/fastme /opt/OrthoFinder/bin/fastme

RUN wget "https://github.com/bbuchfink/diamond/releases/download/v${diamond_version}/diamond-linux64.tar.gz" -O /opt/diamond.tar.gz && \
    tar xvzf /opt/diamond.tar.gz  -C /opt/OrthoFinder/bin/ && \
    rm /opt/diamond.tar.gz

ENV PATH="${PATH}:/opt/OrthoFinder:/opt/OrthoFinder/bin"
