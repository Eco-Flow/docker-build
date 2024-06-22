FROM ubuntu:22.04

ARG datasets_version="v16.1.2"
ARG datasets_architecture="linux-amd64"
ARG earl_version="4.3.0"

# Install dependencies and Miniconda
RUN apt-get update \
    && apt-get install -y wget procps unzip bzip2 build-essential cpanminus \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Install Miniconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh \
    && /bin/bash /tmp/miniconda.sh -b -p /opt/conda \
    && rm /tmp/miniconda.sh \
    && /opt/conda/bin/conda clean -i -l -t -p -y

# Update PATH
ENV PATH="/opt/conda/bin:${PATH}"

# Create writable directories for Conda environments, packages, and cache
RUN mkdir -p /opt/conda/envs /opt/conda/pkgs /opt/conda/cache \
    && chmod -R 777 /opt/conda/envs /opt/conda/pkgs /opt/conda/cache

# Create .condarc file to specify custom envs, pkgs, and cache directories
RUN echo "envs_dirs:\n  - /opt/conda/envs\npkgs_dirs:\n  - /opt/conda/pkgs\ncache_dirs:\n  - /opt/conda/cache" > /root/.condarc

# Create a non-root user and set permissions
RUN useradd -m dockeruser \
    && chown -R dockeruser:dockeruser /opt/conda /root/.condarc

# Switch to non-root user
USER dockeruser
WORKDIR /home/dockeruser

# Install Earlgrey in the Conda environment
RUN conda create -n myenv python=3.9 \
    && conda install -n myenv -c conda-forge libgcc-ng=12 \
    && conda install -n myenv -c bioconda earlgrey=${earl_version} \
    && conda clean -a -y

# Switch back to root to install Perl modules
USER root

# Install Perl File::Which module
RUN cpanm File::Which

# Switch back to non-root user
USER dockeruser

# Set the default shell to bash and activate the Conda environment in a single RUN command
SHELL ["bash", "-c"]

# Use conda init to ensure conda activate works, and activate the environment
RUN conda init bash \
    && echo "source activate myenv" >> /home/dockeruser/.bashrc

# Set the working directory
WORKDIR /workspace

# If you need to run additional commands with the activated environment, use a single RUN command
# RUN conda activate myenv && some_command
