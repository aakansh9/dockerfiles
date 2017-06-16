
FROM aakansh9/gpu-ml:ubuntu14.04-cuda8-cudnn5-devel-p3
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"

RUN apt-get -y update && \

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
    python -m nltk.downloader -d /usr/share/nltk_data all && \
    
    #--------- Stop-words
    pip install stop-words && \

    #--------- HDF5 support
    conda install h5py && \
    
    #--------- https://github.com/biopython/biopython
    pip install biopython && \

    #--------- PUDB for local debugging convenience
    pip install pudb && \
    
    #----CHECK----- Regularized Greedy Forests
    apt-get install zip unzip && \
    cd /usr/local/src && wget https://github.com/fukatani/rgf_python/releases/download/0.2.0/rgf1.2.zip && \
    unzip rgf1.2.zip && cd rgf1.2 && make && mv bin/rgf /usr/local/bin && \
    cd /usr/local/src && git clone https://github.com/fukatani/rgf_python.git && \
    cd rgf_python && \
    python setup.py install && \
    
    #--------- Imbalanced-learn
    cd /usr/local/src && git clone https://github.com/scikit-learn-contrib/imbalanced-learn.git && \
    cd imbalanced-learn && python setup.py install && \

    #--------- Scikit-Learn nightly build
    apt-get -y install build-essential python3-dev python3-setuptools python3-numpy python3-scipy libatlas-dev libatlas3gf-base && \
    cd /usr/local/src && git clone https://github.com/scikit-learn/scikit-learn.git && \
    cd scikit-learn && make && python setup.py install && \

    #--------- Tensorflow (with gpu support)
    cd /usr/local/src && \
    pip install tensorflow && \

    #--------- Spacy for English NLP
    pip install spacy && \
    python -m spacy download en

