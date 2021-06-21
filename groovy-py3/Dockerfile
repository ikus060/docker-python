FROM ubuntu:groovy

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3-pip python3-setuptools python3-nose python3-coverage python3-dev virtualenv tox build-essential git curl wget openssh-client && \
    rm -rf /var/lib/apt/lists/*
