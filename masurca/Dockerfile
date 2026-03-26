FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-c"]

ARG MASURCA_VERSION="4.1.4"

# System dependencies (bash included explicitly for safety)
RUN apt-get update && apt-get install -y \
    bash \
    build-essential \
    gcc \
    g++ \
    make \
    cmake \
    git \
    wget \
    curl \
    perl \
    python3 \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libncurses5-dev \
    libncursesw5-dev \
    libgdbm-dev \
    libssl-dev \
    ca-certificates \
    file \
    procps \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt

# Download MaSuRCA
RUN wget https://github.com/alekseyzimin/masurca/releases/download/v${MASURCA_VERSION}/MaSuRCA-${MASURCA_VERSION}.tar.gz && \
    tar -xzf MaSuRCA-${MASURCA_VERSION}.tar.gz && \
    rm MaSuRCA-${MASURCA_VERSION}.tar.gz

# Build MaSuRCA (handle harmless "same file" error safely)
WORKDIR /opt/MaSuRCA-${MASURCA_VERSION}

RUN set -o pipefail && \
    BOOST_ROOT=install ./install.sh -j$(nproc) 2>&1 | tee build.log || \
    (grep -q "are the same file" build.log)

# Environment
ENV PATH="/opt/MaSuRCA-${MASURCA_VERSION}/bin:$PATH"
ENV PERL5LIB="/opt/MaSuRCA-${MASURCA_VERSION}/lib/perl"

WORKDIR /data
