FROM mambaorg/micromamba:0.13.1

COPY conda.yml conda.here.yml

RUN apt-get update \
    && apt-get install -y wget \
                          procps \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN micromamba install -y -n base -f conda.here.yml && \
    micromamba clean --all --yes