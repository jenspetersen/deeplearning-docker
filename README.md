# deeplearning-docker
Docker image(s) for deep learning

## dl-base
Image containing Anaconda, Theano, Tensorflow, Lasagne, Keras (inspired by https://github.com/floydhub/dl-docker)

## del-conda-env
Image that can be configured with a conda environment file.

## Running a container
You will need:

1. NVIDIA GPU
2. Working NVIDIA driver
3. Docker & NVIDIA Docker installed (https://github.com/NVIDIA/nvidia-docker)

To run (for example):

    nvidia-docker run --rm -p 8888:8888 dl-base jupyter notebook --allow-root

which would let you access a jupyter notebook at localhost:8888 in your browser. Try importing theano from there to see if it recognizes your GPU. If `import theano` is silent, it's only using the CPU.
