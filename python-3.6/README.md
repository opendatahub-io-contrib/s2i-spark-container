# s2i-spark-container

A base image for s2i builds based on Python 3.6 with Java and Spark & Hadoop binaries

## ARGUMENTS
* `SPARK_VERSION` - Version of spark to build from source
* `HADOOP_VERSION` - Version of hadoop to bundle with this spark version
* `JAVA_VERSION` - Version of openjdk to install in this image.
* `SPARK_SOURCE_REPO` - Git repo to clone for the spark source
* `SPARK_SOURCE_REPO_BRANCH` - Git branch to use for the spark build. Defaults to the tagging format used in the Apache Spark repo "v${SPARK_VERSION}"
* `SPARK_SOURCE_REPO_TARGET_DIR` - Directory name to use for the destination clone of the spark repo.
* `SPARK_BUILD_ARGS` - Build arguments that will be passed to the spark `dev/make-distribution.sh`  See [Building a Runnable Distribution](https://spark.apache.org/docs/latest/building-spark.html#building-a-runnable-distribution) for the spark version being built.

```
SPARK_VERSION=2.4.5
HADOOP_VERSION=2.8.5
JAVA_VERSION=1.8.0
SPARK_IMAGE_TAG=spark-${SPARK_VERSION}_hadoop-${HADOOP_VERSION}

# Build the container image that is used as the base image for the jupyter s2i spark notebook
docker build --build-arg ${SPARK_VERSION} --build-arg ${HADOOP_VERSION} --build-arg ${JAVA_VERSION} -t s2i-spark-container:${SPARK_IMAGE_TAG} https://github.com/lavlas/s2i-spark-container.git:python-3.6
```