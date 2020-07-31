FROM buildpack-deps:stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3-pip python3-dev build-essential && \
    pip3 install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
