FROM node:6

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
    ssh \
    curl \
    git \
    vim \
    wget \
    zlib1g-dev \
    jq \
    build-essential \
    iptables \
    libapparmor1 \
    libltdl7 \
    libmcrypt-dev \
    libxml2-dev \
    zip \
    unzip \
    python \
    python-pip \
    python-yaml \
    && apt-get clean

RUN pip install awscli


