FROM rocker/r-base:4.3.1

RUN apt-get update && \
    apt-get install -y procps perl libcurl4-openssl-dev libssl-dev libxml2-dev && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages(c('BiocManager', 'RSQLite'))"

RUN Rscript -e "BiocManager::install('biomaRt')"

CMD ["/bin/bash"]
