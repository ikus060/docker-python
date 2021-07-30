FROM centos:7

Run yum install -y python3-pip python3-devel gcc git && \
  pip3 install virtualenv nose coverage tox --upgrade

RUN yum -y install centos-release-scl-rh && \
  yum -y install rh-python38-python-devel rh-python38-python-tkinter rh-python38-python-pip git gcc && \
  source scl_source enable rh-python38 && \
  pip3 install nose coverage tox --upgrade