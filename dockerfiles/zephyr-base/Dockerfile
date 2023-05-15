FROM ubuntu:20.04
USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt upgrade
RUN apt install -y wget
RUN wget https://apt.kitware.com/kitware-archive.sh && bash kitware-archive.sh
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
RUN python3-pip install west
RUN echo 'export PATH=~/.local/bin:"$PATH"' >> ~/.bashrc
RUN source ~/.bashrc
RUN west init zephyrproject && cd zephyrproject && west update && west zephyr-export
RUN python3.8 -m pip install -r zephyrproject/zephyr/scripts/requirements.txt