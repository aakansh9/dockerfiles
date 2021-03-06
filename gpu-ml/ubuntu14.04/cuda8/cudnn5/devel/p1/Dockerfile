# CUDA 8
# cuDNN 5
# Ubuntu 14.04

FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Install anaconda3
# Following code is from continuumio/anaconda3:latest
# Needs to be maintained by copy-paste from continuumio/anaconda3:latest

RUN apt-get update --fix-missing && apt-get install -y apt-utils wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda3-4.4.0-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh

RUN apt-get update && apt-get install -y curl grep sed dpkg && \
    TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean

ENV PATH /opt/conda/bin:$PATH

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]