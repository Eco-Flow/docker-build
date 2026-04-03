# Stage 1 — build blast2mcl from source
FROM rust:latest AS rust-builder

RUN apt-get update && apt-get install -y --no-install-recommends \
    pkg-config \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN git clone --branch rustblast2mcl --depth 1 \
    https://github.com/chriswyatt1/OrthoFinder /build/OrthoFinder

WORKDIR /build/OrthoFinder/blast2mcl
RUN cargo build --release


# Stage 2 — runtime image
FROM python:3.11-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-dev \
    git \
    procps \
    && rm -rf /var/lib/apt/lists/*

COPY --from=rust-builder /build/OrthoFinder /opt/orthofinder

COPY --from=rust-builder \
    /build/OrthoFinder/blast2mcl/target/release/blast2mcl \
    /opt/orthofinder/src/orthofinder/bin/blast2mcl

RUN chmod +x /opt/orthofinder/src/orthofinder/bin/*

WORKDIR /opt/orthofinder
RUN pip install --no-cache-dir .

ENTRYPOINT ["orthofinder"]
