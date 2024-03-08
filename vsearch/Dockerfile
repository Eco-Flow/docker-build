FROM ubuntu:22.04

RUN apt-get update && apt-get install -y wget

ARG vsearch_version="2.27.0" 

RUN wget "https://github.com/torognes/vsearch/releases/download/v${vsearch_version}/vsearch-${vsearch_version}-linux-x86_64-static.tar.gz" && \
    tar -xvzf "vsearch-${vsearch_version}-linux-x86_64-static.tar.gz" -C /opt && \
    rm "vsearch-${vsearch_version}-linux-x86_64-static.tar.gz"

ENV PATH="${PATH}:/opt/vsearch-${vsearch_version}-linux-x86_64-static/bin"
