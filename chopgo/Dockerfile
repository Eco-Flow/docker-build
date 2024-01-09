FROM rocker/r-base:4.3.1

RUN apt-get update && \
    apt-get install -y python3.10 wget procps && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages(c('BiocManager', 'devtools', 'dplyr', 'readxl', 'writexls', 'plyr', 'gdata', 'pheatmap', 'ashr'))"

RUN Rscript -e "BiocManager::install('RCurl')"

RUN Rscript -e "BiocManager::install('topGO')"
