FROM ambakshi/perforce-base
MAINTAINER Amit Bakshi <ambakshi@gmail.com>

ARG P4_VERSION

RUN echo /etc/yum.conf
RUN sed 's/^timeout=30$/timeout=60/' /etc/yum.conf
RUN echo /etc/yum.conf

RUN yum clean all --enablerepo='*' \
    && yum clean metadata --enablerepo='*' \
    && yum install --enablerepo=perforce -y helix-p4d-20${P4_VERSION} helix-cli-20${P4_VERSION} \
    && yum clean all --enablerepo='*' \
    && rm -rf /var/cache/yum


EXPOSE 1666
ENV NAME p4depot
ENV P4CONFIG .p4config
ENV DATAVOLUME /mnt/p4_volume
ENV P4PORT 1666
ENV P4USER p4admin
VOLUME ["$DATAVOLUME"]

ADD ./p4-users.txt /root/
ADD ./p4-groups.txt /root/
ADD ./p4-protect.txt /root/
ADD ./setup-perforce.sh /usr/local/bin/
ADD ./run.sh  /

CMD ["/run.sh"]
