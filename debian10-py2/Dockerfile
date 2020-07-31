FROM buildpack-deps:buster

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-pip python-dev build-essential && \
    pip2 install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
