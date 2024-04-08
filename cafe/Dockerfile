FROM rocker/r-base:4.3.1

ARG newick_version="1.6"
ARG cafe_version="5.1"

RUN apt-get update && \
    apt-get install -y wget build-essential cmake curl procps gcc make libkrb5-3 libcurl4-openssl-dev python3.11 python3-pip ruby-full cpanminus libdb-dev && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN gem install bio

RUN cpanm CGI
RUN cpanm DBD::SQLite
RUN cpanm DB_File
RUN cpanm URI

RUN Rscript -e "install.packages(c('devtools', 'ape', 'data.table'))"

RUN wget "https://anaconda.org/bioconda/newick_utils/${newick_version}/download/linux-64/newick_utils-${newick_version}-h031d066_7.tar.bz2" && \
    mkdir -p /opt/newick && \
    tar -xjf "newick_utils-${newick_version}-h031d066_7.tar.bz2" -C /opt/newick && \
    rm /"newick_utils-${newick_version}-h031d066_7.tar.bz2"

ENV PATH="${PATH}:/opt/newick/bin"

RUN wget "https://github.com/hahnlab/CAFE5/releases/download/v${cafe_version}/CAFE5-${cafe_version}.0.tar.gz" && \
    tar -xvzf CAFE5-${cafe_version}.0.tar.gz -C /opt && \
    cd /opt/CAFE5 && ./configure && make && \
    rm /CAFE5-${cafe_version}.0.tar.gz

ENV PATH="${PATH}:/opt/CAFE5/bin"
