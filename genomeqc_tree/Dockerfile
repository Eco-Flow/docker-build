FROM rocker/r-base:4.3.3

# Install required system packages including Python
RUN apt-get update && \
    apt-get install -y procps curl libxml2-dev libssl-dev libcurl4-openssl-dev python3 python3-pip && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install pandas using pip
RUN pip3 install pandas

# Create a directory for R libraries with proper permissions
RUN mkdir -p /usr/local/lib/R_user_lib && \
    chmod -R 777 /usr/local/lib/R_user_lib

# Set the R library path to the new directory
ENV R_LIBS_USER=/usr/local/lib/R_user_lib

# Install R packages and BiocManager
RUN Rscript -e "install.packages(c('R.utils', 'BiocManager', 'dplyr', 'ggplot2', 'cowplot', 'argparse'))"

# Install ggtree using BiocManager
RUN Rscript -e "BiocManager::install('ggtree', update = TRUE, ask = FALSE)"
