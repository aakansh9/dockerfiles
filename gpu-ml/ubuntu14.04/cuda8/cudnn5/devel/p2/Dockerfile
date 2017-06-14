# CUDA 8
# cuDNN 5
# Ubuntu 14.04
# anaconda 3

FROM aakansh9/gpu-ml:ubuntu14.04-cuda8-cudnn5-devel-p1
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"

RUN apt-get update && apt-get install -y build-essential && \
    apt-get install -y libfreetype6-dev libglib2.0-0 libxext6 libsm6 libxrender1 libfontconfig1 --fix-missing && \

    # Newer version of Pandas than comes with continuumio/anaconda3
    # conda uninstall -y pandas && pip install pandas && \

    #--------- Tensorflow with GPU support
    cd /usr/local/src && \
    pip install tensorflow-gpu && \

    #--------- Vowpal Wabbit
    apt-get install -y libboost-program-options-dev zlib1g-dev libboost-python-dev && \
    cd /usr/local/src && \
    git clone git://github.com/JohnLangford/vowpal_wabbit.git && \
    cd vowpal_wabbit && make && make install && \
    cd python && pip install -e . && \

    #--------- Some Python Packages
    pip install seaborn python-dateutil dask pytagcloud pyyaml ggplot joblib husl geopy ml_metrics mne pyshp gensim && \
    
    #--------- ImageMagick
    # The apt-get version of imagemagick is out of date and has compatibility issues, so we build from source
    # there is some problem with dbus
    apt-get build-dep imagemagick -y && \
    cd /usr/local/src && wget http://www.imagemagick.org/download/ImageMagick.tar.gz && \
    tar xzf ImageMagick.tar.gz && cd `ls -d ImageMagick-*` && pwd && ls -al && ./configure && \
    make -j $(nproc) && make install && \
    cd ../ && rm -rf ImageMagick*
