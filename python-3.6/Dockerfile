FROM registry.access.redhat.com/ubi8/python-36

USER root
RUN yum -y install java-1.8.0-openjdk maven llvm-toolset llvm-devel &&\
    yum clean all
USER 1001
RUN pip install pyspark==2.4.5 Cython &&\
    pip install numpy scipy
RUN fix-permissions /opt/app-root
