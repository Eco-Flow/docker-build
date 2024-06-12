FROM gitpod/workspace-base

USER root

RUN apt-get update \
    && apt-get install -y procps wget build-essential software-properties-common libcurl4-openssl-dev libssl-dev libexpat1-dev libjpeg-dev zlib1g-dev bzip2 \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install util tools.
# software-properties-common is needed to add ppa support for Apptainer installation
RUN apt-get update --quiet && \
    apt-get install --yes \
        apt-transport-https \
        apt-utils \
        sudo \
        git \
        less \
        wget \
        curl \
        tree 

RUN apt-get update && apt-get install -y --no-install-recommends \
        python3.5 \
        python3-pip \
        && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*
    
RUN pip3 install nibabel pydicom matplotlib pillow