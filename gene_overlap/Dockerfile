FROM rocker/r-base:4.3.3

# Install system dependencies
RUN apt-get update && \
    apt-get install -y \
        procps \
        curl \
        libcurl4-openssl-dev \
        libxml2-dev \
        libssl-dev \
        zlib1g-dev \
        build-essential \
    && apt-get clean

# Create a directory for R libraries with proper permissions
RUN mkdir -p /usr/local/lib/R_user_lib && \
    chmod -R 777 /usr/local/lib/R_user_lib

# Set the R library path to the new directory
ENV R_LIBS_USER=/usr/local/lib/R_user_lib

# Install R packages and BiocManager
RUN Rscript -e "install.packages(c('R.utils', 'BiocManager', 'dplyr', 'ggplot2', 'argparse'))"
RUN Rscript -e "BiocManager::install(c('GenomicRanges', 'IRanges', 'GenomeInfoDb', 'BiocGenerics'))"
