FROM ubuntu:22.04

#Need to buy a copy of pearRM software (free for academics): https://www.h-its.org/software/pear-paired-end-read-merger/
COPY ./pear-0.9.11-linux-x86_64.tar.gz .

RUN tar -xvzf /pear-0.9.11-linux-x86_64.tar.gz -C /opt && rm /pear-0.9.11-linux-x86_64.tar.gz

ENV PATH="${PATH}:/opt/pear-0.9.11-linux-x86_64/bin" 
