FROM rocker/r-base:4.3.3

RUN apt-get update && \
    apt-get install -y procps perl && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages('BiocManager')"

RUN Rscript -e "BiocManager::install('biomaRt')"

CMD ["/bin/bash"]
