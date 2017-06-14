

FROM aakansh9/gpu-ml:ubuntu14.04-cuda8-cudnn5-devel-p2
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"


RUN apt-get -y update && \

    #--------- OpenCV (from source)
    # upgraded cmake is needed, one with apt-get is old
    apt-get -y install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev && \
    apt-get -y install libtbb2 libtbb-dev libjpeg-dev libtiff-dev libjasper-dev && \
    cd /usr/local/src && wget http://www.cmake.org/files/v3.2/cmake-3.2.2.tar.gz && \
    tar xf cmake-3.2.2.tar.gz && cd cmake-3.2.2 && ./configure && make && make install && \ 
    cd /usr/local/src && git clone --depth 1 https://github.com/Itseez/opencv.git && \
    cd opencv && \
    mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_TBB=ON \
          -D WITH_FFMPEG=OFF \
          -D WITH_V4L=ON \
          -D WITH_QT=OFF \
          -D WITH_OPENGL=ON \
          -D PYTHON3_EXECUTABLE=/opt/conda/bin/python3 \
          -D PYTHON3_LIBRARY=/opt/conda/lib/libpython3.6m.so \
          -D PYTHON3_INCLUDE_DIR=/opt/conda/include/python3.6m \
          -D PYTHON_LIBRARY=/opt/conda/lib/libpython3.6m.so \
          -D PYTHON_INCLUDE_DIR=/opt/conda/include/python3.6m \
          -D BUILD_PNG=TRUE .. && \
    make -j $(nproc) && make install && \
    echo "/usr/local/lib/python3.6/site-packages" > /etc/ld.so.conf.d/opencv.conf && ldconfig && \
    cp /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so /opt/conda/lib/python3.6/site-packages/ && \
    # clean up
    rm -rf /usr/local/src/opencv && \
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
