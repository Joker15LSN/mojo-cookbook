ARG BASE_IMAGE=homebrew/ubuntu22.04:latest

FROM ${BASE_IMAGE}

ENV DEBIAN_FRONTEND=noninteractive
ADD sources.list /etc/apt/

USER root
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

RUN curl https://get.modular.com | MODULAR_AUTH=mut_ffab751536ab4957a9729a22be847e6a sh - && \
    modular install mojo && \
    echo 'export MODULAR_HOME="$HOME/.modular"' >> ~/.bashrc && \
    echo 'export PATH="$MODULAR_HOME/pkg/packages.modular.com_mojo/bin:$PATH"' >> ~/.bashrc && \
    /bin/bash -c "source /root/.bashrc"

RUN modular update mojo

RUN pip3 install --no-cache-dir jupyterlab -i https://mirrors.aliyun.com/pypi/simple