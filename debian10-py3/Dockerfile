FROM buildpack-deps:buster

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3-pip python3-setuptools python3-nose python3-coverage python3-dev virtualenv tox build-essential rustc && \
    pip3 install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
