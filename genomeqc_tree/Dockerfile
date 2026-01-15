FROM rocker/r-base:4.3.3

# Install system packages
RUN apt-get update && \
    apt-get install -y \
      procps curl libxml2-dev libssl-dev libtiff-dev fontconfig fonts-liberation libcairo2-dev \
      libcurl4-openssl-dev python3 python3-pip python3-pandas libmagick++-dev libtool libharfbuzz-dev libfribidi-dev \
      r-cran-rcppeigen r-cran-lme4 r-cran-mgcv libfontconfig1-dev libfreetype6-dev bzip2 && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Patch Makeconf to fix the GCC flag
RUN sed -i 's/-std=gnu23/-std=gnu2x/g' /usr/lib/R/etc/Makeconf

# User library
RUN mkdir -p /usr/local/lib/R_user_lib && chmod -R 777 /usr/local/lib/R_user_lib
ENV R_LIBS_USER=/usr/local/lib/R_user_lib

# For systemfonts
ENV PKG_CONFIG_PATH=/usr/lib/x86_64-linux-gnu/pkgconfig

# Install first batch of R packages for better caching
RUN Rscript -e "install.packages(c('R.utils', 'httpuv', 'shiny', 'BiocManager', 'cowplot', 'dplyr', 'tidyr', 'ggplot2'))"

# Install second batch of R packages
RUN Rscript -e "install.packages(c('argparse', 'patchwork', 'scatterpie', 'scales','textshaping', 'svglite'))"

# Install ggtree
RUN Rscript -e "BiocManager::install(c('ggtree'), update = FALSE, ask = FALSE)"

RUN mkdir /app

CMD cd /app; Rscript shiny_app.R
