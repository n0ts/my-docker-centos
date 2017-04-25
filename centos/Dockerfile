FROM centos:latest

MAINTAINER Naoya Nakazawa <naoya.n@gmail.com>

ENV user centos
ENV group centos
ENV work /work

RUN \
    yum clean all \
    && yum install -y epel-release \
    && yum upgrade -y \
    && yum groupinstall -y "Development Tools" \
    && yum install -y bash-completion \
                      curl emacs git \
                      less the_silver_searcher \
                      sudo tree unzip vim wget zsh \

    # add local user
    && groupadd ${user} \
    && useradd ${user} -g ${group} -m -s /bin/bash \
    && echo "%${group} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/00-${group} \
    && chmod 400 /etc/sudoers.d/00-${group} \

    # create work directory
    && mkdir ${work} \
    && chown -R ${user}:${group} ${work}

CMD ["/bin/bash"]
