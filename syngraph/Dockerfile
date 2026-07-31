# Syngraph (https://github.com/A-J-F-Mackintosh/syngraph) -- parsimony-based
# ancestral linkage group (ALG) inference across a phylogeny, used by the
# Eco-Flow/synteny pipeline's ALGO subworkflow.
#
# Targets Python 3.8 with fairly old pinned dependencies (networkx==2.4,
# numpy==1.20.3, graph-tool, ete3, pygraphviz...). Upstream's yaml/syngraph.yaml
# is a full `conda env export` snapshot pinned to exact build hashes from
# ~2022, which no longer solves against current channel indices -- this
# instead follows the looser install command documented in their README,
# which lets conda pick currently-available builds satisfying the same
# version constraints.
#
# Only linux-64 (amd64) conda builds of graph-tool etc. are available, hence
# the explicit --platform below regardless of build host (Docker/BuildKit
# will emulate on arm64 hosts such as Apple Silicon). Deliberately hardcoded,
# not $TARGETPLATFORM -- ignore a linter's "should not use a constant" hint
# here, that's exactly what's wanted.
FROM --platform=linux/amd64 continuumio/miniconda3:24.7.1-0

# Pinned to the commit this recipe was last tested against. Syngraph has no
# tagged releases; bump deliberately (and re-test modules/local/algo/syngraph.nf
# in Eco-Flow/synteny) rather than silently floating to whatever master is
# on a rebuild.
ARG SYNGRAPH_COMMIT=1df1f6bc37c254cfb163bf9ce08ee30e375fe32c

RUN git clone https://github.com/A-J-F-Mackintosh/syngraph.git /opt/syngraph \
    && cd /opt/syngraph \
    && git checkout ${SYNGRAPH_COMMIT}

# continuumio/miniconda3 already ships procps (`ps`), which Nextflow needs for
# task metrics -- confirmed present, no extra install needed here.

RUN conda create -y -n syngraph -c etetoolkit -c conda-forge -c bioconda -c defaults \
        python=3.8 \
        pandas \
        docopt \
        ete3 \
        pygraphviz \
        matplotlib \
        tqdm \
        "networkx=2.4" \
        "numpy=1.20.3" \
        "pillow<10" \
        more-itertools \
    && conda clean -afy

ENV PATH="/opt/conda/envs/syngraph/bin:/opt/syngraph:${PATH}"

# The repo's main entrypoint script is `syngraph` at the repo root (invoked as
# `syngraph <module> ...`) -- confirm this still matches if SYNGRAPH_COMMIT
# is ever bumped, and adjust PATH/permissions if it moves.
RUN chmod +x /opt/syngraph/syngraph

WORKDIR /data
