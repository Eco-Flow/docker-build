# AGORA (https://github.com/DyogenIBENS/Agora) -- ancestral gene order
# reconstruction, used by the Eco-Flow/synteny pipeline's ALGO subworkflow.
#
# Upstream ships its own multi-stage Dockerfile pinned to python:3.7.7-slim +
# requirements.txt (just `psutil`). This mirrors that base image/dependency
# rather than re-deriving it, using a single stage since a slim final image
# isn't a priority here.
FROM python:3.7.7-slim

# python:3.7.7-slim is based on Debian buster, which is EOL and has been
# moved to archive.debian.org -- repoint apt there before installing anything.
RUN sed -i \
        -e 's|deb.debian.org/debian |archive.debian.org/debian |g' \
        -e 's|security.debian.org/debian-security|archive.debian.org/debian-security|g' \
        -e '/buster-updates/d' \
        /etc/apt/sources.list \
    && apt-get -o Acquire::Check-Valid-Until=false update \
    && apt-get install -y --no-install-recommends git procps \
    && rm -rf /var/lib/apt/lists/*
# procps (`ps`) is required for Nextflow task metrics -- python:3.7.7-slim
# does not ship it by default.

# Pinned to the commit this recipe was last tested against. Bump deliberately
# (and re-test modules/local/algo/agora.nf in Eco-Flow/synteny) rather than
# silently floating to whatever master is on a rebuild -- AGORA's own docs
# were found to be incomplete/misleading about its real input requirements
# (see Eco-Flow/synteny's ALGO subworkflow notes), so a version bump here
# needs re-validating against a real run, not just a successful build.
ARG AGORA_COMMIT=f9dd78faab145bacb1808ed468b37c3cfb84fadd

RUN git clone https://github.com/DyogenIBENS/Agora.git /opt/agora \
    && cd /opt/agora \
    && git checkout ${AGORA_COMMIT} \
    && pip install --no-cache-dir -r requirements.txt

RUN chmod +x /opt/agora/src/*.py
ENV PATH="/opt/agora/src:${PATH}"

WORKDIR /data
