FROM rocker/r-base:4.3.3

# Install required packages
RUN apt-get update && \
    apt-get install -y procps curl && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install R packages
RUN Rscript -e "install.packages(c('R.utils', 'dplyr', 'hash'))"
RUN Rscript -e "install.packages(c('dada2', 'ShortRead', 'beepr', 'Biostrings'))"

# Install Mambaforge (a smaller and faster version of Miniconda)
RUN mkdir -p /opt/software && \
    cd /opt/software && \
    curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh" && \
    bash Mambaforge-Linux-x86_64.sh -b -p /opt/software/mambaforge && \
    rm Mambaforge-Linux-x86_64.sh

# Initialize conda
RUN /opt/software/mambaforge/bin/conda init && \
    /opt/software/mambaforge/bin/conda config --set auto_activate_base false

# Add conda to PATH
ENV PATH=/opt/software/mambaforge/bin:$PATH

# Configure conda to use bioconda and conda-forge channels
RUN conda config --add channels bioconda && \
    conda config --add channels conda-forge

# Install cutadapt
RUN conda install -y cutadapt

# Set up default command
CMD ["R"]
