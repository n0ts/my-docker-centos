FROM n0ts/centos-python

MAINTAINER Naoya Nakazawa <naoya.n@gmail.com>

ENV user centos
ENV group centos

RUN set -x \
    && yum install -y python2-boto python2-boto3 python-passlib openssl-devel ansible \
    && pip install ansible-lint \
    && pip install --upgrade ansible \

    # install human_log callback plugin
    # https://github.com/n0ts/ansible-human_log/
    && mkdir -p /usr/share/ansible/plugins/callback \
    && curl -L -o /etc/ansible/ansible.cfg \
        https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg \
    && curl -L -o /etc/ansible/hosts \
        https://raw.githubusercontent.com/ansible/ansible/devel/examples/hosts \

    # change ansible configuration
    && sed -i 's/#retry_files_enabled = False/retry_files_enabled = False/g' /etc/ansible/ansible.cfg \
    && sed -i 's/#library        = \/usr\/share\/my_modules\//library = \/ansible\/modules/g' /etc/ansible/ansible.cfg \
    && sed -i 's/sudo_user      = root/become_user      = root/g' /etc/ansible/ansible.cfg \

    # add ansible user & group
    && groupadd ansible \
    && gpasswd -a ${user} ansible \
    && mkdir -m 770 /var/log/ansible \
    && touch /var/log/ansible/ansible.log \
    && chmod 660 /var/log/ansible/ansible.log \
    && chown -v -R root:${group} /var/log/ansible \
    && sed -i 's/#log_path = \/var\/log\/ansible.log/log_path = \/var\/log\/ansible\/ansible.log/g' /etc/ansible/ansible.cfg \

    && yum clean all \

    && ansible-lint --version \
    && ansible --version

CMD ["/bin/bash"]
