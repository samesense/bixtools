FROM ubuntu:18.04

MAINTAINER Daniel Miller <millerd15@email.chop.edu>

ENV TRUVARI_VERSION 1.3.4

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y python3 python3-pip && \
    pip3 install Truvari==${TRUVARI_VERSION} 
