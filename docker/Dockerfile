FROM nvidia/cuda:9.0-devel

RUN ln -fs /usr/share/zoneinfo/Europe/Moscow /etc/localtime
RUN apt-get update && \
    apt install -yq \
        vim \
        sudo \
        wget \
        curl \
        build-essential \
        cmake \
        git \
        ca-certificates \
        libjpeg-dev \
        zip \
        unzip \
        libpng-dev \
        libeigen3-dev \
        libglfw3-dev \
        libglfw3 \
        libgoogle-glog-dev \
        libsuitesparse-dev \
        libatlas-base-dev \
        libsm6 \
        libxrender1 \
        libfontconfig1 \
        libgoogle-glog-dev \
        libsuitesparse-dev \
        libatlas-base-dev \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# (mini)conda
# https://repo.anaconda.com/miniconda/
RUN wget -q https://repo.anaconda.com/miniconda/Miniconda3-py37_4.8.3-Linux-x86_64.sh && \
    sh ./Miniconda3-py37_4.8.3-Linux-x86_64.sh -b -p /opt/conda && \
    rm ./Miniconda3-py37_4.8.3-Linux-x86_64.sh && \
    export PATH=$PATH:/opt/conda/bin && \
    conda install conda-build

ENV PATH $PATH:/opt/conda/envs/env/bin:/opt/conda/bin
ENV CUDA_HOME /usr/local/cuda

RUN conda init bash && \
    conda create -n pvnet python=3.7 && \
    . /opt/conda/etc/profile.d/conda.sh && \
    conda activate pvnet && \
    pip install torch==1.1.0 -f https://download.pytorch.org/whl/cu90/stable && \
    pip install Cython==0.28.2

RUN . /opt/conda/etc/profile.d/conda.sh && \
    conda activate pvnet && \
    pip install jupyter ipykernel && \
    python -m ipykernel install --name pvnet

CMD . /opt/conda/etc/profile.d/conda.sh && \
    conda activate pvnet && \
		jupyter notebook --allow-root --ip 0.0.0.0

