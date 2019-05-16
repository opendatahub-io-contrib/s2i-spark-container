FROM registry.access.redhat.com/ubi7/python-27

USER root
RUN yum -y install java-1.8.0-openjdk pandoc &&\
    yum clean all
USER 1001
RUN . /opt/app-root/etc/scl_enable && pip install --upgrade wheel pip && pip install pyspark==2.2.*
RUN fix-permissions /opt/app-root
