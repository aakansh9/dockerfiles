
FROM aakansh9/gpu-ml:ubuntu14.04-cuda8-cudnn5-devel-p4
LABEL maintainer "AAKANSH GUPTA <aakansh9+contact@gmail.com>"

RUN apt-get -y update && \

    # Anaconda's build of gcc is way out of date; monkey-patch some linking problems that affect
    # packages like xgboost and Shapely
    #rm /opt/conda/lib/libstdc++* && rm /opt/conda/lib/libgomp.* && \
    #ln -s /usr/lib/x86_64-linux-gnu/libgomp.so.1 /opt/conda/lib/libgomp.so.1 && \
    #ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 /opt/conda/lib/libstdc++.so.6 && \
    
    #----- Libgeos (for mapping libraries)
    apt-get -y install libgeos-dev && \
    
    #----- Basemap (plot on map projections using matplotlib)
    pip install pyshp pyproj && \
    cd /usr/local/src && git clone https://github.com/matplotlib/basemap.git && \
    export GEOS_DIR=/usr/local && \
    cd basemap && python setup.py install && \
    
    #----- Pillow (PIL)
    apt-get -y install zlib1g-dev liblcms2-dev libwebp-dev && \
    pip install Pillow && \

    #----- Ibis
    apt-get -y install libsasl2-dev && \
    apt-get install -y libpq-dev && \
    pip install ibis-framework && \

    #----- Cartopy + Shapely
    yes | conda install proj4 && \
    pip install packaging && \
    cd /usr/local/src && git clone https://github.com/Toblerity/Shapely.git && \
    cd Shapely && python setup.py install && \
    cd /usr/local/src && git clone https://github.com/SciTools/cartopy.git && \
    cd cartopy && python setup.py install && \

    #----- Set matplotlib backend to Agg
    matplotlibrc_path=$(python -c "import site, os, fileinput; packages_dir = site.getsitepackages()[0]; print(os.path.join(packages_dir, 'matplotlib', 'mpl-data', 'matplotlibrc'))") && \
    sed -i 's/^backend      : Qt5Agg/backend      : Agg/' $matplotlibrc_path  && \
    
    #----- Stop jupyter nbconvert trying to rewrite its folder hierarchy
    mkdir -p /root/.jupyter && touch /root/.jupyter/jupyter_nbconvert_config.py && touch /root/.jupyter/migrated && \
    mkdir -p /.jupyter && touch /.jupyter/jupyter_nbconvert_config.py && touch /.jupyter/migrated && \
    
    #----- Stop Matplotlib printing junk to the console on first load
    sed -i "s/^.*Matplotlib is building the font cache using fc-list.*$/# Warning removed by Kaggle/g" /opt/conda/lib/python3.6/site-packages/matplotlib/font_manager.py && \
    
    #----- Make matplotlib output in Jupyter notebooks display correctly
    mkdir -p /etc/ipython/ && echo "c = get_config(); c.IPKernelApp.matplotlib = 'inline'" > /etc/ipython/ipython_config.py && \

    #----- Convex Optimization library
    pip install cvxopt && \

    #----- Profiling and other utilities
    pip install line_profiler && \
    pip install orderedmultidict && \
    pip install smhasher && \
    conda install -y -c bokeh datashader && \

    #----- Boruta (python implementation)
    cd /usr/local/src && git clone https://github.com/danielhomola/boruta_py.git && \
    cd boruta_py && python setup.py install && \

    #----- LightGBM
    cd /usr/local/src && git clone --recursive --depth 1 https://github.com/Microsoft/LightGBM && \
    cd LightGBM && mkdir build && cd build && cmake .. && make -j $(nproc) && \
    cd /usr/local/src/LightGBM/python-package && python setup.py install && \

    #----- pyeconometrics
    cd /usr/local/src && git clone git://github.com/nicolashennetier/pyeconometrics.git && \
    cd pyeconometrics && python setup.py install && \

    #----- graphviz
    apt-get install -y graphviz && pip install graphviz && \

    #----- pydot-ng (python interface to graphviz language)
    cd /usr/local/src && git clone git://github.com/pydot/pydot-ng.git && \
    cd pydot-ng && python setup.py install && \

    #----- fiona + geopandas
    apt-get install -y libgdal1-dev && GDAL_CONFIG=/usr/bin/gdal-config pip install fiona && \
    pip install geopandas && \

    #----- py-earth
    cd /usr/local/src && git clone git://github.com/scikit-learn-contrib/py-earth.git && \
    cd py-earth && python setup.py install && \

    # ~~~~ CLEAN UP ~~~~
    rm -rf /root/.cache/pip/* && \
    apt-get autoremove -y && apt-get clean && \
    conda clean -i -l -t -y && \
    rm -rf /usr/local/src/*

    