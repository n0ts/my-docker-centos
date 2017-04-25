FROM n0ts/centos

MAINTAINER Naoya Nakazawa <naoya.n@gmail.com>

RUN \
  yum install -y python-pip python-devel python-virtualenv \
  && pip install --upgrade pip \
  && python --version \
  && pip --version

CMD ["/bin/bash"]
