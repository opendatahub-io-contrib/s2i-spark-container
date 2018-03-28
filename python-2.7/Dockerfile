FROM centos/python-27-centos7

USER root
RUN yum -y install java-1.8.0-openjdk &&\
    yum clean all
USER 1001
RUN . /opt/app-root/etc/scl_enable && pip install pyspark==2.2.*
RUN fix-permissions /opt/app-root
