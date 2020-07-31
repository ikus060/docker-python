FROM buildpack-deps:stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-pip python-setuptools python-dev build-essential && \
    pip2 install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
