FROM amazonlinux:2.0.20240223.0
LABEL maintainer="opensource@khulnasoft.com"
ENV container=docker

RUN yum makecache fast \
 && yum -y install deltarpm epel-release initscripts \
 && yum -y update \
 && yum -y install \
      sudo \
      which \
      python-pip \
      cronie \
 && yum clean all

VOLUME ["/sys/fs/cgroup"]
CMD ["/usr/lib/systemd/systemd"]
