FROM rocker/r-base:4.3.1

RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-pandas wget procps libcurl4-openssl-dev libssl-dev perl && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages(c('BiocManager', 'devtools', 'dplyr', 'tidyr','readxl', 'writexls', 'plyr', 'gdata', 'pheatmap', 'ashr', 'ggplot2', 'ggstar', 'scatterpie', 'scales'))"

RUN Rscript -e "BiocManager::install('RCurl')"

RUN Rscript -e "BiocManager::install('topGO')"

ARG newick_version="1.6"

RUN wget "https://anaconda.org/bioconda/newick_utils/${newick_version}/download/linux-64/newick_utils-${newick_version}-h031d066_7.tar.bz2" && \
    mkdir -p /opt/newick && \
    tar -xjf "newick_utils-${newick_version}-h031d066_7.tar.bz2" -C /opt/newick && \
    rm /"newick_utils-${newick_version}-h031d066_7.tar.bz2"

ENV PATH="${PATH}:/opt/newick/bin"

RUN Rscript -e "install.packages('R.utils')"
