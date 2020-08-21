FROM buildpack-deps:bullseye

# pip, nose are not available in bulleye
RUN apt-get update && \
    apt-get install -y --no-install-recommends python-setuptools python-coverage python-dev virtualenv tox build-essential && \
    wget https://bootstrap.pypa.io/get-pip.py && \
    python2 get-pip.py  && \
    pip install nose --upgrade && \
    rm -rf /var/lib/apt/lists/*
