FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y wget procps ruby-full mysql-server gcc libexpat1-dev libcurl4-openssl-dev libssl-dev \
    zlib1g-dev libdb-dev libmysqlclient-dev vim bzip2 git curl make python libdbd-mysql-perl cpanminus && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/* 

RUN cpanm JSON::XS
RUN cpanm Module::Build
RUN cpanm Bit::Vector
RUN cpanm SVG
RUN cpanm Term::ReadKey
RUN cpanm Time::HiRes
RUN cpanm DBI
RUN cpanm XML::Parser
RUN cpanm Carp::Clan
RUN cpanm Class::Inspector
RUN cpanm HTML::Parser
RUN cpanm LWP
RUN cpanm SOAP::Lite
RUN cpanm URI
RUN cpanm Inline
RUN cpanm Inline::C
RUN cpanm Parse::RecDescent
RUN cpanm version
RUN cpanm DB_File


RUN gem install gnuplot
RUN gem install narray
RUN gem install RubyInline

RUN wget "https://github.com/maasha/biopieces/archive/refs/tags/2.0.tar.gz" -O /biopieces.tar.gz && \
    tar xvzf /biopieces.tar.gz -C /opt && \
    rm /biopieces.tar.gz

RUN cat >~/.bashrc <<EOL
# >>>>>>>>>>>>>>>>>>>>>>> Enabling Biopieces if installed <<<<<<<<<<<<<<<<<<<<<<<

# Modify the below paths according to your settings.

export BP_DIR="/opt/biopieces-2.0"  # Directory where biopieces are installed
export BP_DATA="$HOME/BP_DATA"   # Contains genomic data etc.
export BP_TMP="$HOME/tmp"        # Required temporary directory.
export BP_LOG="$HOME/BP_LOG"     # Required log directory.

if [ -f "/opt/biopieces-2.0/config/bashrc" ]; then
    source "/opt/biopieces-2.0/config/bashrc"
fi

# >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
EOL

RUN mkdir "${HOME}/BP_DATA" "${HOME}/tmp" "${HOME}/BP_LOG"

RUN git clone https://github.com/maasha/biopieces.wiki.git /opt/biopieces-2.0/wiki

RUN apt-get update && \
    apt-get install -y subversion && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/* 
