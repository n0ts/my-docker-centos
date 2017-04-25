FROM n0ts/centos-python

MAINTAINER Naoya Nakazawa <naoya.n@gmail.com>

ENV user centos
ENV group centos

RUN \
  yum install -y python2-boto python2-boto3 python-passlib openssl-devel ansible \
  && pip install ansible-lint \
  && pip install --upgrade ansible \
  && mkdir -p /usr/share/ansible/plugins/callback \
  && wget -N \
       https://raw.githubusercontent.com/n0ts/ansible-human_log/master/human_log.py \
       -P /usr/share/ansible/plugins/callback/ \
  && sed -i 's/#retry_files_enabled = False/retry_files_enabled = False/g' /etc/ansible/ansible.cfg \
  && sed -i 's/#library        = \/usr\/share\/my_modules\//library = \/ansible\/modules/g' /etc/ansible/ansible.cfg \
  && sed -i 's/sudo_user      = root/become_user      = root/g' /etc/ansible/ansible.cfg \
  && groupadd ansible \
  && gpasswd -a ${user} ansible \
  && mkdir -m 770 /var/log/ansible \
  && touch /var/log/ansible/ansible.log \
  && chmod 660 /var/log/ansible/ansible.log \
  && chown -v -R root:${group} /var/log/ansible \
  && sed -i 's/#log_path = \/var\/log\/ansible.log/log_path = \/var\/log\/ansible\/ansible.log/g' /etc/ansible/ansible.cfg \
  && ansible --version

CMD ["/bin/bash"]