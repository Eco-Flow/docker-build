FROM ubuntu:22.04

ARG datasets_version="v16.1.2"
ARG datasets_architecture="linux-amd64"

ARG earl_version="4.3.0"

# Install dependencies and Miniconda
RUN apt-get update \
    && apt-get install -y wget procps unzip bzip2 \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Install Miniconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh \
    && /bin/bash /tmp/miniconda.sh -b -p /opt/conda \
    && rm /tmp/miniconda.sh \
    && /opt/conda/bin/conda clean -i -l -t -p -y

# Update PATH
ENV PATH="/opt/conda/bin:${PATH}"

# Create a new environment with Python 3.9 and install Earlgrey
RUN conda create -n myenv python=3.9 \
    && conda install -n myenv -c conda-forge libgcc-ng=12 \
    && conda install -n myenv -c bioconda earlgrey=${earl_version} \
    && conda clean -a -y

# Set the default shell to bash and activate the Conda environment in a single RUN command
SHELL ["bash", "-c"]

# Use conda init to ensure conda activate works, and activate the environment
RUN conda init bash \
    && echo "conda activate myenv" >> ~/.bashrc

# Set the working directory
WORKDIR /workspace
