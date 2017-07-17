FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04

MAINTAINER Jens Petersen <jens.petersen@dkfz.de>

RUN apt-get update && apt-get install -y \
		build-essential \
		cmake \
		curl \
		git \
		nano \
		pkg-config \
		software-properties-common \
		unzip \
		vim \
		wget

# Install Miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh -O miniconda.sh && \
		bash miniconda.sh -b -p /root/miniconda2 && \
		rm miniconda.sh
ENV PATH=/root/miniconda2/bin:$PATH

# Install conda environment packages
COPY environment.yml /root/
RUN conda env update -n root -f /root/environment.yml && rm /root/environment.yml

# Install virtualenv environment packages
COPY requirements.txt /root/
RUN pip install -r /root/requirements.txt && rm /root/requirements.txt

WORKDIR "/root"
CMD ["/bin/bash"]
