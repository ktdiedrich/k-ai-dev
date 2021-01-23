FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04 
# FROM tensorflow/tensorflow:latest-gpu-py3-jupyter

USER root 

ENV DEBIAN_FRONTEND=noninteractive 
ENV DEBCONF_NONINTERACTIVE_SEEN=true
ENV OPT=/opt 
ENV CONDA_HOME=${OPT}/miniconda
ENV TMP=/tmp

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils 

RUN apt-get update && apt-get install -y --no-install-recommends \
    libnotify4 \
    libnss3 \
    libxkbfile1 \
    libsecret-1-0 \
    libgtk-3-0 \
    wget \
    git \ 
    ssh \
    emacs \
    vim \
    less \ 
    file \
    postgresql \
    postgresql-client \
    golang-go \
    nginx \
    libfcgi-dev \
    spawn-fcgi \
    python3-tk \
    gconf2 \ 
    gvfs-bin \
    xdg-utils \
    libcurl4 \ 
    curl \
    openjdk-8-jre-headless \
    openjdk-8-jdk \
    mongodb \
    python3-pip \
    python3-pymongo \
    python3-flask-mongoengine \
    gnupg \
    cmake \ 
    cmake-gui \
    libgl1 \ 
    unzip \
    mesa-utils \
    libgl1-mesa-glx \
    gdb \
    eog \ 
    graphviz \
    gdebi-core \
    gdebi \
    ############## not compatible with libssl-dev 
    # libssl1.0-dev  \
    # nodejs \
    # nodejs-dev \
    # npm \
    ############## ITK, VTK require libssl-dev
    libssl-dev \
    libcpprest-dev
    # libdcmtk-dev \
    # default-libmysqlclient-dev \
    # libmysqlclient-dev \
    # libgdal-dev \
    # vtk7 \ 
    # libvtk7-dev \ 
    # libvtkgdcm2-dev \ 
    # libvtkgdcm-tools \
    # vtk7-examples \
    # insighttoolkit4-examples \
    # libinsighttoolkit4.12 
    # libinsighttoolkit4-dev

WORKDIR ${TMP}
RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ${TMP}/miniconda.sh && \
    /bin/bash ${TMP}/miniconda.sh -b -p ${CONDA_HOME} && \
    # wget --quiet https://packages.microsoft.com/repos/vscode/pool/main/c/code/code_1.45.1-1589445302_amd64.deb -O ${TMP}/code.deb && \
    curl -o ${TMP}/code.deb -fSL https://go.microsoft.com/fwlink/?LinkID=760868 && \
    gdebi -n -q ${TMP}/code.deb && \
    wget --quiet https://dbeaver.io/files/dbeaver-ce_latest_amd64.deb -O ${TMP}/dbeaver.deb && \
    gdebi -n -q ${TMP}/dbeaver.deb
     # && \
    # rm ${TMP}/*.sh && \
    # rm ${TMP}/*.deb
 # wget --quiet https://atom.io/download/deb -O ${TMP}/atom.deb && \ 
 #   dpkg -i ${TMP}/atom.deb && apt-get install -f && \


WORKDIR ${OPT}
RUN wget --quiet https://download.jetbrains.com/python/pycharm-community-2020.1.1.tar.gz?_ga=2.1894769.1984017565.1590319299-433175914.1590319299 -O ${OPT}/pycharm-ce.tar.gz && \ 
    tar -xvzf ${OPT}/pycharm-ce.tar.gz
    # && \
    # ln -svf ${OPT}/pycharm-community-2020.1.1/bin/pycharm.sh /usr/local/bin/pycharm.sh && \
    # wget --quiet https://download.pytorch.org/libtorch/nightly/cpu/libtorch-shared-with-deps-latest.zip -O ${OPT}/libtorch-shared-with-deps-latest.zip && \
    # unzip ${OPT}/libtorch-shared-with-deps-latest.zip && \
    # wget --quiet https://github.com/QIICR/dcmqi/releases/download/latest/dcmqi-1.2.2-linux-20200602-3efde87.tar.gz -O ${OPT}/dcmqi.tar.gz && \
    # tar -xvzf ${OPT}/dcmqi.tar.gz && \
    # ln -svf ${OPT}/dcmqi-1.2.2-linux-20200602-3efde87 ${OPT}/dcmqi && \
    # rm ${OPT}/*.gz
    # && \
    # rm ${OPT}/*.zip


ENV Torch_DIR=${OPT}/libtorch/share/cmake/Torch/
ENV PATH=${CONDA_HOME}/bin:${OPT}/dcmqi/bin:${PATH}

# ADD Postman-linux-x64-7.25.0.tar.gz ${OPT}/
# RUN ln -svf /opt/Postman/Postman /usr/local/bin/Postman  

# RUN npm install -g create-react-app
EXPOSE 8899
EXPOSE 5006
ADD launch_jupyter_notebook.sh /usr/local/bin
ENV DISPLAY=":0"

ADD environment-conda.yml ${TMP}/
RUN conda env update -f ${TMP}/environment-conda.yml

# RUN pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/cuda/10.0 nvidia-dali
RUN ln -svf ${OPT}/pycharm-community-2020.1.1/bin/pycharm.sh /usr/local/bin/pycharm.sh
RUN ln -svf $CONDA_HOME/lib/libopenh264.so.2.1.1 $CONDA_HOME/lib/libopenh264.so.5

