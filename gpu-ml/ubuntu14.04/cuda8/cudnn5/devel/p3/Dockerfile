

FROM aakansh9/python-ml1
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
    
    echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf && ldconfig && \
    #echo "/usr/local/lib/python3.6/site-packages" > /etc/ld.so.conf.d/opencv.conf && ldconfig && \
    cp /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so /opt/conda/lib/python3.6/site-packages/ && \
    # clean up
    rm -rf /usr/local/src/opencv && \
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    # solve an import cv2 issue
    apt-get -y update && cd / && conda install -y libgcc

    #--------- textblob
    pip install textblob && \

    #--------- word cloud
    pip install git+git://github.com/amueller/word_cloud.git && \
    
    #--------- igraph
    pip install python-igraph && \
    
    #--------- xgboost
    cd /usr/local/src && mkdir xgboost && cd xgboost && \
    git clone --depth 1 --recursive https://github.com/dmlc/xgboost.git && cd xgboost && \
    make && cd python-package && python setup.py install && \

    #--------- Base ATLAS plus tSNE
    # NOTE: we provide the tsne package, but sklearn.manifold.TSNE now does the same job
    apt-get install -y libatlas-base-dev && \
    cd /usr/local/src && git clone --depth 1 https://github.com/danielfrg/tsne.git && \
    cd tsne && python setup.py install && \

    #--------- Levenshtein Python C extension module
    cd /usr/local/src && git clone --depth 1 https://github.com/ztane/python-Levenshtein && \
    cd python-Levenshtein && python setup.py install && \

    #--------- ML for High Energy Physics
    cd /usr/local/src && git clone --depth 1 https://github.com/arogozhnikov/hep_ml.git && \
    cd hep_ml && pip install . && \
    
    #--------- NLTK Project datasets
    mkdir -p /usr/share/nltk_data && \
    python -m nltk.downloader -d /usr/share/nltk_data all
    
    #--------- Stop-words
    pip install stop-words && \

    #--------- HDF5 support
    conda install h5py && \
    
    #--------- https://github.com/biopython/biopython
    pip install biopython && \

    #--------- PUDB for local debugging convenience
    pip install pudb && \
    
    #----FAIL----- Regularized Greedy Forests
    apt-get install zip unzip && \
    cd /usr/local/src && wget https://github.com/fukatani/rgf_python/releases/download/0.2.0/rgf1.2.zip && \
    unzip rgf1.2.zip && cd rgf1.2 && make && mv bin/rgf /usr/local/bin && \
    cd /usr/local/src && git clone https://github.com/fukatani/rgf_python.git && \
    cd rgf_python && sed -i 's/\/opt\/rgf1.2\/bin\/rgf/\/usr\/local\/bin\/rgf/' rgf/rgf.py && \
    python setup.py install && \
    

    
    #--------- Imbalanced-learn
    cd /usr/local/src && git clone https://github.com/scikit-learn-contrib/imbalanced-learn.git && \
    cd imbalanced-learn && python setup.py install && \

    #-----FAIL---- Scikit-Learn nightly build
    apt-get -y install build-essential python3-dev python3-setuptools python3-numpy python3-scipy libatlas-dev libatlas3gf-base && \
    cd /usr/local/src && git clone https://github.com/scikit-learn/scikit-learn.git && \
    cd scikit-learn && python setup.py build && python setup.py install && \























RUN 

    # Tensorflow -- add gpu support
    #cd /usr/local/src && \
    #pip install tensorflow && \

    
    #python -m spacy.en.download && \

    # ImageMagick [ Debian vs Ubuntu problems ]
    apt-get -y install imagemagick && \

    # OpenCV
    apt-get -y install libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev && \
    apt-get -y install libtbb2 libtbb-dev libjpeg-dev libtiff-dev libjasper-dev && \
    apt-get -y install cmake && \
    cd /usr/local/src && git clone --depth 1 https://github.com/Itseez/opencv.git && \
    cd opencv && \
    mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_FFMPEG=OFF -D WITH_V4L=ON -D WITH_QT=OFF -D WITH_OPENGL=ON -D PYTHON3_LIBRARY=/opt/conda/lib/libpython3.6m.so -D PYTHON3_INCLUDE_DIR=/opt/conda/include/python3.6m/ -D PYTHON_LIBRARY=/opt/conda/lib/libpython3.6m.so -D PYTHON_INCLUDE_DIR=/opt/conda/include/python3.6m/ -D BUILD_PNG=TRUE .. && \
    make -j $(nproc) && make install && \
    echo "/usr/local/lib/python3.6/site-packages" > /etc/ld.so.conf.d/opencv.conf && ldconfig && \
    cp /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so /opt/conda/lib/python3.6/site-packages/ && \
    # Clean up
    rm -rf /usr/local/src/opencv && \
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean

RUN 
    
    #lasagne
    cd /usr/local/src && mkdir Lasagne && cd Lasagne && \
    git clone --depth 1 https://github.com/Lasagne/Lasagne.git && cd Lasagne && \
    pip install -r requirements.txt && python setup.py install && \
    
    #keras
    cd /usr/local/src && mkdir keras && cd keras && \
    git clone --depth 1 https://github.com/fchollet/keras.git && \
    cd keras && python setup.py install && \
    
    #keras-rl
    cd /usr/local/src && mkdir keras-rl && cd keras-rl && \
    git clone --depth 1 https://github.com/matthiasplappert/keras-rl.git && \
    cd keras-rl && python setup.py install && \
    
    #neon
    cd /usr/local/src && \
    git clone --depth 1 https://github.com/NervanaSystems/neon.git && \
    cd neon && pip install -e . && \
    #nolearn
    cd /usr/local/src && mkdir nolearn && cd nolearn && \
    git clone --depth 1 https://github.com/dnouri/nolearn.git && cd nolearn && \
    echo "x" > README.rst && echo "x" > CHANGES.rst && \
    python setup.py install && \
    
    # Dev branch of Theano
    pip install git+git://github.com/Theano/Theano.git --upgrade --no-deps && \
    # put theano compiledir inside /tmp (it needs to be in writable dir)
    printf "[global]\nbase_compiledir = /tmp/.theano\n" > /.theanorc && \
    cd /usr/local/src &&  git clone --depth 1 https://github.com/pybrain/pybrain && \
    cd pybrain && python setup.py install && \
    
    
    # chainer
    pip install chainer && \

    cd /usr/local/src && python cache_keras_weights.py && \
    
    # clean up
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    rm -rf /usr/local/src/*

	# Install OpenCV-3 with Python support
RUN apt-get update && \
    # Anaconda's build of gcc is way out of date; monkey-patch some linking problems that affect
    # packages like xgboost and Shapely
    rm /opt/conda/lib/libstdc++* && rm /opt/conda/lib/libgomp.* && \
    ln -s /usr/lib/x86_64-linux-gnu/libgomp.so.1 /opt/conda/lib/libgomp.so.1 && \
    ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 /opt/conda/lib/libstdc++.so.6 && \
    
    # Libgeos, for mapping libraries
    apt-get -y install libgeos-dev && \
    
    # pyshp and pyproj are now external dependencies of Basemap
    pip install pyshp pyproj && \
    cd /usr/local/src && git clone https://github.com/matplotlib/basemap.git && \
    export GEOS_DIR=/usr/local && \
    cd basemap && python setup.py install && \
    
    # Pillow (PIL)
    apt-get -y install zlib1g-dev liblcms2-dev libwebp-dev && \
    pip install Pillow && \
    cd /usr/local/src && git clone https://github.com/vitruvianscience/opendeep.git && \
    cd opendeep && python setup.py develop  && \
    
    # sasl is apparently an ibis dependency
    apt-get -y install libsasl2-dev && \
    
    # ...as is psycopg2
    apt-get install -y libpq-dev && \
    pip install ibis-framework && \
    
    # Cartopy plus dependencies
    yes | conda install proj4 && \
    pip install packaging && \
    cd /usr/local/src && git clone https://github.com/Toblerity/Shapely.git && \
    cd Shapely && python setup.py install && \
    cd /usr/local/src && git clone https://github.com/SciTools/cartopy.git && \
    cd cartopy && python setup.py install && \
    
    # MXNet
    cd /usr/local/src && git clone --recursive https://github.com/dmlc/mxnet && \
    cd /usr/local/src/mxnet && cp make/config.mk . && \
    sed -i 's/ADD_LDFLAGS =/ADD_LDFLAGS = -lstdc++/' config.mk && \
    make && cd python && python setup.py install && \
    
    # set backend for matplotlib to Agg
    matplotlibrc_path=$(python -c "import site, os, fileinput; packages_dir = site.getsitepackages()[0]; print(os.path.join(packages_dir, 'matplotlib', 'mpl-data', 'matplotlibrc'))") && \
    sed -i 's/^backend      : Qt5Agg/backend      : Agg/' $matplotlibrc_path  && \
    
    # Stop jupyter nbconvert trying to rewrite its folder hierarchy
    mkdir -p /root/.jupyter && touch /root/.jupyter/jupyter_nbconvert_config.py && touch /root/.jupyter/migrated && \
    mkdir -p /.jupyter && touch /.jupyter/jupyter_nbconvert_config.py && touch /.jupyter/migrated && \
    
    # Stop Matplotlib printing junk to the console on first load
    sed -i "s/^.*Matplotlib is building the font cache using fc-list.*$/# Warning removed by Kaggle/g" /opt/conda/lib/python3.6/site-packages/matplotlib/font_manager.py && \
    
    # Make matplotlib output in Jupyter notebooks display correctly
    mkdir -p /etc/ipython/ && echo "c = get_config(); c.IPKernelApp.matplotlib = 'inline'" > /etc/ipython/ipython_config.py && \
    
    # h2o
    # This requires python-software-properties and Java.
    apt-get install -y python-software-properties zip && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list &&     echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list &&     apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 C857C906 2B90D010 && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    cd /usr/local/src && mkdir h2o && cd h2o && \
    wget http://h2o-release.s3.amazonaws.com/h2o/latest_stable -O latest && \
    wget --no-check-certificate -i latest -O h2o.zip && rm latest && \
    unzip h2o.zip && rm h2o.zip && cp h2o-*/h2o.jar . && \
    pip install `find . -name "*whl"` && \
    
    # Keras setup
    # Keras likes to add a config file in a custom directory when it's
    # first imported. This doesn't work with our read-only filesystem, so we
    # have it done now
    python -c "from keras.models import Sequential"  && \
    
    # Switch to TF backend
    sed -i 's/theano/tensorflow/' /root/.keras/keras.json  && \
    
    # Re-run it to flush any more disk writes
    python -c "from keras.models import Sequential; from keras import backend; print(backend._BACKEND)" && \
    # Keras reverts to /tmp from ~ when it detects a read-only file system
    mkdir -p /tmp/.keras && cp /root/.keras/keras.json /tmp/.keras && \
    

    

    
    # Convex Optimization library
    # Latest version fails to install, see https://github.com/cvxopt/cvxopt/issues/77
    #    and https://github.com/cvxopt/cvxopt/issues/80
    # pip install cvxopt && \
    # Profiling and other utilities
    pip install line_profiler && \
    pip install orderedmultidict && \
    pip install smhasher && \
    conda install -y -c bokeh datashader && \
    # Boruta (python implementation)
    cd /usr/local/src && git clone https://github.com/danielhomola/boruta_py.git && \
    cd boruta_py && python setup.py install && \
    cd /usr/local/src && git clone --recursive --depth 1 https://github.com/Microsoft/LightGBM && \
    cd LightGBM && mkdir build && cd build && cmake .. && make -j $(nproc) && \
    cd /usr/local/src/LightGBM/python-package && python setup.py install && \
    cd /usr/local/src && git clone git://github.com/nicolashennetier/pyeconometrics.git && \
    cd pyeconometrics && python setup.py install && \
    apt-get install -y graphviz && pip install graphviz && \
    apt-get install -y libgdal1-dev && GDAL_CONFIG=/usr/bin/gdal-config pip install fiona && pip install geopandas && \
    cd /usr/local/src && git clone git://github.com/scikit-learn-contrib/py-earth.git && \
    cd py-earth && python setup.py install && \
    # ~~~~ CLEAN UP ~~~~
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    conda clean -i -l -t -y && \
    rm -rf /usr/local/src/*

    ###########
    #
    #      NEW CONTRIBUTORS:
    # Please add new pip/apt installs in this block. Don't forget a "&& \" at the end
    # of all non-final lines. Thanks!
    #
    ###########
RUN pip install --upgrade mpld3 && \
    pip install mplleaflet && \
    pip install gpxpy && \
    pip install arrow && \
    pip install sexmachine  && \
    pip install Geohash && \
    pip install deap && \
    pip install tpot && \
    pip install haversine && \
    pip install toolz cytoolz && \
    pip install sacred && \
    pip install plotly && \
    pip install git+https://github.com/nicta/dora.git && \
    pip install git+https://github.com/hyperopt/hyperopt.git && \
    # tflean. Deep learning library featuring a higher-level API for TensorFlow. http://tflearn.org
    pip install git+https://github.com/tflearn/tflearn.git && \
    pip install fitter && \
    pip install langid && \
    # Delorean. Useful for dealing with datetime
    pip install delorean && \
    pip install trueskill && \
    pip install heamy && \
    pip install vida && \
    # Useful data exploration libraries (for missing data and generating reports)
    pip install missingno && \
    pip install pandas-profiling && \
    pip install s2sphere && \
    pip install git+https://github.com/fmfn/BayesianOptimization.git && \
    pip install matplotlib-venn && \
    pip install pyldavis && \
    # Pattern not yet Py3 compatible...
    # pip install pattern && \
    pip install git+git://github.com/rasbt/mlxtend.git#egg=mlxtend && \
    pip install altair && \
    pip install pystan && \
    pip install ImageHash && \
    pip install git+https://github.com/hammerlab/fancyimpute.git && \
    pip install git+https://github.com/pymc-devs/pymc3 && \
    pip install tifffile && \
    pip install spectral && \
    pip install descartes && \
    pip install geojson && \
    pip install pysal && \
    #conda install -y gdal && \
    pip install pyflux && \
    pip install terminalplot && \
    pip install raccoon && \
    pip install pydicom && \
    pip install wavio && \
    pip install SimpleITK && \
    pip install hmmlearn && \
    pip install bayespy && \
    pip install gplearn && \
    pip install PyAstronomy && \
    conda install pytorch torchvision -c soumith && \
    pip install squarify && \
    pip install fuzzywuzzy && \
    pip install python-louvain && \
    pip install pyexcel-ods && \
    pip install sklearn-pandas && \
    pip install stemming && \
    pip install fbprophet && \
    conda install -y -c conda-forge -c ioam holoviews && \
    pip install git+https://github.com/ioam/geoviews.git && \
    pip install hypertools && \
    pip install nxviz && \
    pip install py_stringsimjoin && \
    pip install speedml && \
    pip install nibabel && \
    pip install mlens && \
  
    ##### ^^^^ Add new contributions above here
    # clean up pip cache
    rm -rf /root/.cache/pip/* && \
    # Required to display Altair charts in Jupyter notebook
    jupyter nbextension install --user --py vega