FROM ubuntu:22.04

# Install required dependencies
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    cmake \
    g++ \
    libstdc++-12-dev \  
    zlib1g-dev \
    libz-dev \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /opt

# Clone the repository and initialize submodules
RUN git clone --recurse-submodules https://github.com/comprna/RATTLE.git

# Ensure submodules are initialized (extra safety)
RUN cd RATTLE && git submodule update --init --recursive

# Build spoa manually
RUN sed -i '1i #include <stdexcept>' RATTLE/spoa/src/alignment_engine.cpp
RUN cd RATTLE/spoa && mkdir -p build && cd build && cmake .. -DCMAKE_CXX_STANDARD=17 && make


# Set working directory to RATTLE
WORKDIR /opt/RATTLE

# Run build script
RUN chmod +x build.sh && ./build.sh

# Set environment
ENV PATH="/opt/RATTLE:$PATH"

# Default command
CMD ["bash"]
