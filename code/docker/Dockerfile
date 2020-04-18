FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04 
# FROM tensorflow/tensorflow:latest-gpu-py3-jupyter

USER root 

ENV DEBIAN_FRONTEND=noninteractive 
ENV DEBCONF_NONINTERACTIVE_SEEN=true

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils 

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    libnotify4 \
    libnss3 \
    libxkbfile1 \
    libsecret-1-0 \
    libgtk-3-0 \
    libxss1 \
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
    nodejs \
    nodejs-dev \
    python3-tk \
    gconf2 \ 
    gvfs-bin \
    xdg-utils \
    libcurl4 \ 
    curl \
    openjdk-8-jre-headless \
    npm \
    mongodb \
    python3-pip \
    python3-pymongo \
    python3-flask-mongoengine \
    gnupg 

RUN curl -o /tmp/miniconda.sh -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    chmod +x /tmp/miniconda.sh && \ 
    /tmp/miniconda.sh -b -p /opt/miniconda && \
    rm /tmp/miniconda.sh 

ENV PATH=/opt/miniconda/bin:${PATH}

RUN conda install -y -q -c anaconda setuptools && \ 
    conda install -y -q -c pytorch pytorch torchvision cudatoolkit=10.0 && \
    conda install -y -q -c fastai fastai && \
    conda install -y -q -c conda-forge nvidia-apex && \ 
    conda install -y -q -c anaconda tensorflow-gpu tensorboard && \
    conda install -c conda-forge pycocotools && \
    conda install -c conda-forge albumentations
    
ADD code_1.33.1-1554971066_amd64.deb atom-amd64.deb dbeaver-ce_6.1.2_amd64.deb /tmp/
ADD pycharm-community-2019.1.1.tar.gz Postman-linux-x64-7.2.2.tar.gz /opt/  
RUN ln -svf /opt/pycharm-community-2019.1.1/bin/pycharm.sh /usr/local/bin/pycharm.sh && \
    ln -svf /opt/Postman/Postman /usr/local/bin/Postman 

RUN dpkg -i /tmp/code_1.33.1-1554971066_amd64.deb && apt-get install -f && \ 
    dpkg -i /tmp/atom-amd64.deb && apt-get install -f && \
    dpkg -i /tmp/dbeaver-ce_6.1.2_amd64.deb && apt-get install -f 

RUN pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/cuda/10.0 nvidia-dali

RUN npm install -g create-react-app
ADD requirements.txt /tmp/
RUN /opt/miniconda/bin/pip install -r /tmp/requirements.txt
EXPOSE 8899
EXPOSE 5006
ADD launch_jupyter_notebook.sh /usr/local/bin
ENV DISPLAY=":0"
RUN rm /tmp/*.deb 
