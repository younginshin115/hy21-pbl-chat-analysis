FROM nvidia/cuda:11.2.2-cudnn8-runtime-ubuntu18.04

ENV DEBIAN_FRONTEND noninteractive

ARG SPARK_VERSION=3.1.2
ARG HADOOP_VERSION=3.2
ARG PYTHON_VERSION=3.8.3

RUN apt-get -y update && apt-get -y upgrade && \
    apt-get -y install --no-install-recommends \
    wget tar bash curl vim \
    build-essential checkinstall \
    libreadline-gplv2-dev libncursesw5-dev libssl-dev \
    libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev liblzma-dev \
    openjdk-8-jdk \
    gcc+ \
    git

COPY start-master.sh /start-master.sh
COPY start-worker.sh /start-worker.sh

RUN wget https://mirror.navercorp.com/apache/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz

RUN tar -zxvf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} /spark && \
    rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN tar -xvf Python-${PYTHON_VERSION}.tgz && \
    cd Python-${PYTHON_VERSION} && \
    ./configure --enable-optimizations && \
    make install && \
    apt-get install -y python3-pip && \
    cd ..

ENV PYSPARK_PYTHON=python3

RUN wget https://bitbucket.org/eunjeon/mecab-ko/downloads/mecab-0.996-ko-0.9.2.tar.gz && \
    tar -zxvf mecab-0.996-ko-0.9.2.tar.gz && \
    cd mecab-0.996-ko-0.9.2 && \
    ./configure && make && make install && \
    cd ..

RUN wget https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/mecab-ko-dic-2.1.1-20180720.tar.gz && \
    tar -zxvf mecab-ko-dic-2.1.1-20180720.tar.gz && \
    cd mecab-ko-dic-2.1.1-20180720 && \
    ldconfig && \
    ./configure && make && make install && \
    cd ..

RUN git clone https://bitbucket.org/eunjeon/mecab-python-0.996.git && \
    cd mecab-python-0.996/ && \
    python3 setup.py build && \
    python3 setup.py install

RUN chmod +x /start-master.sh
RUN chmod +x /start-worker.sh
WORKDIR /spark

COPY . /spark

ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/usr/local/cuda/include:/usr/local/cuda/lib64

RUN pip3 install --upgrade pip && \
    pip3 install --upgrade setuptools && \
    pip3 install --no-cache-dir -r requirements.txt