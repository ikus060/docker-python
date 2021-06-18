FROM buildpack-deps:bullseye

ENV DEBIAN_FRONTEND=noninteractive

# pip, nose are not available in bulleye
RUN apt-get update && \
    apt-get install -y --no-install-recommends python-setuptools python-pip-whl python-dev virtualenv tox build-essential rustc && \
    pip install nose coverage --upgrade && \
    rm -rf /var/lib/apt/lists/*
