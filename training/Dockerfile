FROM gitpod/workspace-base

USER root

# Install util tools.
# software-properties-common is needed to add ppa support for Apptainer installation
RUN apt-get update --quiet && \
    apt-get install --yes \
        apt-transport-https \
        apt-utils \
        sudo \
        git \
        less \
        wget \
        curl \
        tree

RUN apt-get update && apt-get remove -y python && apt-get install -y python3 r-base

# Install nextflow and nf-test
RUN /usr/local/bin/curl -s https://get.nextflow.io | bash
RUN /usr/bin/chmod +x nextflow
RUN sudo mv nextflow /usr/local/bin

# Install R and python


# Change user to gitpod
USER gitpod

# Uncomment if we need to pin the Nextflow version
ENV NXF_EDGE=1
ENV NXF_VER=24.02.0-edge
 
# Update Nextflow
RUN nextflow self-update && nextflow -version

RUN unset JAVA_TOOL_OPTIONS

RUN export PS1='\t -> '
