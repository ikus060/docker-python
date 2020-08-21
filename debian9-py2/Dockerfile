FROM buildpack-deps:stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-pip python-setuptools python-nose python-coverage python-dev virtualenv tox build-essential && \
    rm -rf /var/lib/apt/lists/*
