
FROM aakansh9/gpu-ml:ubuntu14.04-cuda8-cudnn5-devel-p5
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"


RUN apt-get -y update && \

    #----- some terminal tools
    apt-get -y install htop tmux vim && \

    #----- libgpuarray + pygpu
    apt-get install -y gfortran liblapack-dev libopenblas-dev && \
    cd /usr/local/src && \
    yes | conda install -c conda-forge pygpu && \

    #----- pycuda
    pip install pycuda && \

    #----- skcuda (dev version)
    pip install git+https://github.com/lebedov/scikit-cuda.git#egg=scikit-cuda && \

    #----- Dev branch of Theano
    cd /usr/local/src/ && pip install git+git://github.com/Theano/Theano.git --upgrade --no-deps && \
    # put theano compiledir inside /tmp (it needs to be in writable dir)
    printf "[global]\nbase_compiledir = /tmp/.theano\n" > /.theanorc && \

    #----- pybrain
    cd /usr/local/src &&  git clone --depth 1 https://github.com/pybrain/pybrain && \
    cd pybrain && python setup.py install && \
    
    #---NOT WORKING-- OpenDeep
    cd /usr/local/src && git clone https://github.com/vitruvianscience/opendeep.git && \
    cd opendeep && python setup.py develop  && \
    
    #----- lasagne
    cd /usr/local/src && mkdir Lasagne && cd Lasagne && \
    git clone --depth 1 https://github.com/Lasagne/Lasagne.git && cd Lasagne && \
    pip install -r requirements.txt && python setup.py install && \
    
    #----- neon
    cd /usr/local/src && \
    git clone --depth 1 https://github.com/NervanaSystems/neon.git && \
    cd neon && make sysinstall && \

    #----- nolearn
    cd /usr/local/src && mkdir nolearn && cd nolearn && \
    git clone --depth 1 https://github.com/dnouri/nolearn.git && cd nolearn && \
    echo "x" > README.rst && echo "x" > CHANGES.rst && \
    python setup.py install && \

    #----- chainer
    pip install cupy && \
    pip install chainer && \
    
    #----- MXNet
    apt-get -y update && apt-get install -y libopenblas-dev libopencv-dev && \
    cd /usr/local/src && git clone --recursive https://github.com/dmlc/mxnet && \
    cd mxnet && cp make/config.mk . && \
    sed -i 's/USE_BLAS = atlas/USE_BLAS = openblas/g' config.mk && \
    sed -i 's/USE_CUDA = 0/USE_CUDA = 1/g' config.mk && \
    sed -i 's/USE_CUDA_PATH = NONE/USE_CUDA_PATH = \/usr\/local\/cuda/g' config.mk && \
    sed -i 's/USE_CUDNN = 0/USE_CUDNN = 1/g' config.mk && \
    make && cd python && python setup.py install && \

    #----- Keras
    apt-get install -y libhdf5-dev python-h5py python-yaml && \
    cd /usr/local/src && mkdir keras && cd keras && \
    git clone --depth 1 https://github.com/fchollet/keras.git && \
    cd keras && python setup.py install && \
    
    #----- keras-rl
    cd /usr/local/src && mkdir keras-rl && cd keras-rl && \
    git clone --depth 1 https://github.com/matthiasplappert/keras-rl.git && \
    cd keras-rl && python setup.py install && \

    #----- h2o
    # This requires python-software-properties and Java.
    apt-get install -y python-software-properties zip && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list &&     echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list &&     apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 C857C906 2B90D010 && \
    apt-get -y update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    cd /usr/local/src && mkdir h2o && cd h2o && \
    wget http://h2o-release.s3.amazonaws.com/h2o/latest_stable -O latest && \
    wget --no-check-certificate -i latest -O h2o.zip && rm latest && \
    unzip h2o.zip && rm h2o.zip && cp h2o-*/h2o.jar . && \
    pip install `find . -name "*whl"`


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
    yes | conda install pytorch torchvision -c soumith && \
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

    #----- clean up
    cd /usr/local/ && rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    rm -rf /usr/local/src/* && \

    # Required to display Altair charts in Jupyter notebook
    jupyter nbextension install --user --py vega

