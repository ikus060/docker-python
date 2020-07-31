FROM buildpack-deps:bullseye

RUN apt-get update && \
    apt-get install -y --no-install-recommends python-pip python-setuptools python-dev build-essential && \
    pip install virtualenv nose coverage tox --upgrade && \
    rm -rf /var/lib/apt/lists/*
