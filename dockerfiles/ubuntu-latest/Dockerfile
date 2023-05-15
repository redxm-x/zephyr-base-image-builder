FROM ubuntu:20.04
USER root

RUN apt update
RUN apt upgrade
RUN apt install -y gcc \ 
                   gzip \
                   firefox \
                   cmake \
                   make

RUN hostname