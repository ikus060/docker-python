FROM buildpack-deps:buster

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3-pip python-setuptools python3-dev build-essential && \
    pip3 install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
