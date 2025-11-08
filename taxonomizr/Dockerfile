FROM rocker/r-ver:4.3.2

RUN apt-get update && \
    apt-get install -y procps && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*
    
RUN Rscript -e "install.packages('taxonomizr', repos='https://cloud.r-project.org')"