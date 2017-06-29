

A collection of dockerfiles for flexible Deep Learning experimentation on GPUs.

## CREDITS

This project is mainly inspired from Kaggle's Docker build at https://github.com/Kaggle/docker-python.
A lot of code has been copy pasted and modified to support Nvidia GPUs through nvidia-docker.
There are also excerpts from Kaixhin's dockerfiles at https://github.com/Kaixhin/dockerfiles.

## Motivation

Setting up a Machine Learning environment for experimentation is a time consuming task. Kaggle's docker build provides an excellent environment with almost all necessary packages. However, it lacks GPU support. Providing GPU support was the main motivation.


## Dockerfiles

Large dockerfiles have usually been partitioned into smaller dockerfiles which are built on each other.
We will try to provide support for all major versions of Ubuntu, CUDA, cuDNN in the future.

## Build

Automated builds have not been enabled yet. But we try to update frequently on Docker Hub. All dockerfiles are built and tested on p2.xlarge instances.

You can also build docker images on your own using the following steps -

1. Install Docker

```sh
sudo apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
sudo apt-key fingerprint 0EBFCD88 && \
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable" && \
sudo apt-get -y update && \
sudo apt-get -y install docker-ce && \
sudo docker run --rm hello-world # testing
```

2. Install nvidia-drivers

```sh
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub && \
sudo sh -c 'echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/cuda.list' && \
sudo apt-get update && sudo apt-get install -y --no-install-recommends linux-headers-generic dkms cuda-drivers && \
nvidia-smi -q | head # check drivers work
```

3. Install nvidia-docker

```sh
wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.1/nvidia-docker_1.0.1-1_amd64.deb && \
sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb && \
nvidia-docker run --rm nvidia/cuda nvidia-smi # test nvidia-docker
```

4. (Optional) Optimize Gpu clock for K80 GPUs on p2.xlarge instances.

```sh
sudo nvidia-smi -pm 1 # configure GPU settings to be persistent
sudo nvidia-smi --auto-boost-default=0 # diable autoboost
sudo nvidia-smi -ac 2505,875 # set GPU clock to max frequency
```

5. Build Docker images

Enter the directory containing the dockerfile and do 

```sh
nvidia-docker build .
docker tag [imagename] aakansh9/cuda8-cudnn5-ubuntu14.04-anaconda3:latest
docker login
docker push aakansh9/cuda8-cudnn5-ubuntu14.04-anaconda3:latest
```

## What is Included

Everything included in Kaggle's Docker build is included. This includes - 

- Python3 Anaconda environment
- All major Deep Learning frameworks
- All major Machine Learning libraries
- All major Statistical libraries
- All major visualizing tools

Please check the dockerfile for specifics.

## CONTRIBUTING

If you face a problem or have contributions in mind, please do not hesitate to raise an issue.
All suggestions are welcome!

