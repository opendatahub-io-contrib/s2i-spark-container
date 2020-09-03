FROM quay.io/thoth-station/s2i-thoth-ubi8-py36:v0.15.0

ARG SPARK_VERSION=2.4.5
ARG HADOOP_VERSION=2.8.5
ARG JAVA_VERSION=1.8.0
ARG SPARK_SOURCE_REPO=https://github.com/apache/spark.git
ARG SPARK_SOURCE_REPO_BRANCH=v${SPARK_VERSION}
ARG SPARK_SOURCE_REPO_TARGET_DIR=spark
ARG SPARK_BUILD_ARGS="-Phive -Phive-thriftserver -Pkubernetes -Dhadoop.version=${HADOOP_VERSION}"

USER root
# Install openjdk so we can build the hadoop jars
RUN yum -y install java-$JAVA_VERSION-openjdk maven &&\
    yum clean all
ENV JAVA_HOME=/usr/lib/jvm/jre

USER 1001
# Build the Apache spark and hadoop binaries from source
# After the build is complete create and install the python wheel file using pip
RUN git clone ${SPARK_SOURCE_REPO} -b ${SPARK_SOURCE_REPO_BRANCH} ${SPARK_SOURCE_REPO_TARGET_DIR}
RUN cd ${SPARK_SOURCE_REPO_TARGET_DIR} &&\
    dev/make-distribution.sh --name spark-${SPARK_VERSION}-hadoop-${HADOOP_VERSION} ${SPARK_BUILD_ARGS}
RUN cd ${SPARK_SOURCE_REPO_TARGET_DIR}/python && python setup.py bdist_wheel && pip install dist/*whl &&\
    cd ${HOME} && rm -rf ${SPARK_SOURCE_REPO_TARGET_DIR}

RUN fix-permissions /opt/app-root
