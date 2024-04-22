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
        tree \
        python3 \
        r-base

#Install java
ENV JAVA_VERSION=17
RUN apt-get update &&  apt-get install -y \
    openjdk-${JAVA_VERSION}-jdk \
    && rm -rf /var/lib/apt/lists/*

# Install nextflow 
RUN curl -s https://get.nextflow.io | bash
RUN chmod +x nextflow
RUN sudo mv nextflow /usr/local/bin/nextflow

#Install nf-test
RUN curl -fsSL https://code.askimed.com/install/nf-test | bash
RUN sudo mv nf-test /usr/local/bin/nf-test

# User permissions
RUN mkdir -p /workspace/data \
    && chown -R gitpod:gitpod /workspace/data

# Change user to gitpod
USER gitpod

RUN unset JAVA_TOOL_OPTIONS

RUN export PS1='\t -> '
