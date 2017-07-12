FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04

MAINTAINER Jens Petersen <jens.petersen@dkfz.de>

# Theano & PyGPU are conda installs, Keras & Lasagne are pip git installs
ARG vAnaconda=4.4.0
ARG vTensorflow=1.2.0
ARG vTheano=0.9.0
ARG vPyGPU=0.6.8
ARG vKeras=1.2.0
ARG vLasagne=master

RUN cat /proc/driver/nvidia/version && nvcc -V

RUN apt-get update && apt-get install -y \
		bc \
		build-essential \
		cmake \
		curl \
		git \
		libopenblas-dev \
		nano \
		pkg-config \
		software-properties-common \
		unzip \
		vim \
		wget \
		yasm \
		doxygen \
		&& \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/* && \
# Link BLAS library to use OpenBLAS using the alternatives mechanism (https://www.scipy.org/scipylib/building/linux.html#debian-ubuntu)
	update-alternatives --set libblas.so.3 /usr/lib/openblas-base/libblas.so.3

# Install Anaconda
RUN wget https://repo.continuum.io/archive/Anaconda2-${vAnaconda}-Linux-x86_64.sh -O anaconda.sh && \
		bash anaconda.sh -b -p /root/anaconda2 && \
		rm anaconda.sh
ENV PATH=/root/anaconda2/bin:$PATH

# Install Tensorflow
RUN pip install --no-cache-dir https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-${vTensorflow}-cp27-none-linux_x86_64.whl

# Install Theano
RUN conda install theano=${vTheano} pygpu=${vPyGPU} && \
	echo "[global]\nfloatX=float32\ndevice=cuda" > /root/.theanorc

# Install Keras
RUN pip --no-cache-dir install git+git://github.com/fchollet/keras.git@${vKeras}

# Install Lasagne
RUN pip --no-cache-dir install git+git://github.com/Lasagne/Lasagne.git@${vLasagne}

# Set up notebook config
COPY jupyter_notebook_config.py /root/.jupyter/
COPY run_jupyter.sh /root/

# Expose Ports for TensorBoard (6006), Ipython (8888)
EXPOSE 6006 8888

WORKDIR "/root"
CMD ["/bin/bash"]
