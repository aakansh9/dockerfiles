
This build is divided into several dockerfiles.

To build enter the current directory and do -

```sh
nvidia-docker build .
docker tag [imagename] aakansh9/cuda8-cudnn5-ubuntu14.04-anaconda3:latest
docker login
docker push aakansh9/cuda8-cudnn5-ubuntu14.04-anaconda3:latest
```