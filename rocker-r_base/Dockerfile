FROM rocker/r-base:4.3.3

RUN apt-get update && \
    apt-get install -y procps && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages(c('R.utils', 'dplyr'))"
