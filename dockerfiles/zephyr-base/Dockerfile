FROM ubuntu:20.04
USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN mkdir /tmp/zephyr
RUN apt update
RUN apt upgrade
RUN apt install -y wget
RUN wget -O /tmp/zephyr/kitware-archive.sh https://apt.kitware.com/kitware-archive.sh
RUN bash /tmp/zephyr/kitware-archive.sh
RUN apt install -y --no-install-recommends git \ 
                                           cmake \ 
                                           ninja-build \ 
                                           gperf \ 
                                           ccache \
                                           dfu-util \ 
                                           device-tree-compiler \
                                           wget \ 
                                           python3-dev \
                                           python3-pip \
                                           python3-setuptools \
                                           python3-tk python3-wheel \
                                           xz-utils file \
                                           make \
                                           gcc \
                                           gcc-multilib \
                                           g++-multilib \
                                           libsdl2-dev \
                                           libmagic1


RUN cmake --version
RUN python3 --version
RUN dtc --version
RUN apt install -y python3-venv
RUN python3.8 -m pip install west
RUN echo 'export PATH=~/.local/bin:"$PATH"' >> ~/.bashrc
RUN . ~/.bashrc && \
    west init /tmp/zephyr/zephyrproject && \ 
    cd /tmp/zephyr/zephyrproject && \
    west update && \ 
    west zephyr-export && \
    python3.8 -m pip install -r zephyrproject/zephyr/scripts/requirements.txt
RUN wget -O /tmp/zephyr/zephyr-sdk-0.16.1_linux-x86_64.tar.xz https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.1/zephyr-sdk-0.16.1_linux-x86_64.tar.xz
RUN cd /tmp/zephyr && wget -O - https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.1/sha256.sum | shasum --check --ignore-missing