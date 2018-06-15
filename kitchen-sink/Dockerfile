FROM ubuntu:16.04
ARG tf_version="0.11.7"
ARG go_version="1.10.3"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    dmsetup \
    git \
    gzip \
    jq \
    make \
    python-pip \
    software-properties-common \
    unzip \
    wget \
    zip \
    redis-server \
    default-jdk \
    build-essential checkinstall \
    libssl-dev \
    && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Docker
RUN ( curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - ) \
 && apt-key fingerprint 0EBFCD88 \
 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
 && apt-get update \
 && apt-get install -y docker-ce

# SBT
RUN ( echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list ) \
 && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 \
 && apt-get update \
 && apt-get install -y --no-install-recommends sbt

# Node
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash - \
 && apt-get install -y nodejs \
 && npm install -g yarn

# AWS CLI
RUN pip install -U setuptools wheel \
&& pip install -U awscli

# Terraform 
RUN curl https://releases.hashicorp.com/terraform/${tf_version}/terraform_${tf_version}_linux_amd64.zip -o terraform_${tf_version}_linux_amd64.zip \
    && unzip terraform_${tf_version}_linux_amd64.zip -d /usr/local/bin \
    && rm terraform_${tf_version}_linux_amd64.zip 

# GoLang
RUN curl https://dl.google.com/go/go${go_version}.linux-amd64.tar.gz -o go${go_version}.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go${go_version}.linux-amd64.tar.gz \
    && rm go${go_version}.linux-amd64.tar.gz 

RUN mkdir -p ${HOME}/go \
    && echo 'export GOPATH=${HOME}/go' >> ${HOME}/.profile \
    && echo 'export GOBIN=${GOPATH}/bin' >> ${HOME}/.profile

ENV PATH=$PATH:/usr/local/go/bin

# Cleanup
RUN rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*


