FROM python:3.10-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential \
    software-properties-common libz-dev procps wget && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

#Removing newer version of setuptools that is causing issues
RUN rm -rf /usr/lib/python3/dist-packages/setuptools*

#"setuptools<58.0.0" stops pyVCF use_2to3 error
RUN pip install --no-cache-dir "setuptools~=57.5.0"

RUN pip install --no-cache-dir \
    boto3 awscli pyfaidx pyliftover pyvcf \
    cython pandas scipy matplotlib scikit-image pypdf2 wand Pillow jcvi

ARG last_version='1522'

RUN wget "https://gitlab.com/mcfrith/last/-/archive/1522/last-${last_version}.tar.gz" && \
    tar -xf "last-${last_version}.tar.gz" -C /opt && \
    cd "/opt/last-${last_version}" && \
    make && \
    rm "/last-${last_version}.tar.gz"
