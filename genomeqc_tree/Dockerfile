FROM rocker/r-base:4.3.3

# Install required system packages including Python
RUN apt-get update && \
    apt-get install -y procps curl libxml2-dev libssl-dev libcurl4-openssl-dev python3 python3-pip && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install R packages and BiocManager
RUN Rscript -e "install.packages(c('R.utils', 'BiocManager', 'dplyr', 'ggplot2', 'cowplot'))"

# Install ggtree using BiocManager
RUN Rscript -e "BiocManager::install('ggtree', update = TRUE, ask = FALSE)"

# Set up default command
CMD ["R"]
