Bootstrap: docker
From: nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04

%environment

	#Use bash as default shell
	SHELL=/bin/bash

	#Add nvidia driver paths

	PATH="/nvbin:$PATH"
	LD_LIBRARY_PATH="/nvlib:$LD_LIBRARY_PATH"

	#Add CUDA paths

	CPATH="/usr/local/cuda/include:$CPATH"
	PATH="/usr/local/cuda/bin:$PATH"
	LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
	CUDA_HOME="/usr/local/cuda"

	export PATH LD_LIBRARY_PATH CPATH CUDA_HOME


%setup
	#Runs on host
	#The path to the image is $SINGULARITY_ROOTFS



%post
	#Post setup script

	#Default mount paths
	mkdir /scratch /data /shared /fastdata

	#Nvidia Library mount paths
	mkdir /nvlib /nvbin

  #Updating and getting required packages
  apt-get update
  apt-get install -y wget git vim

  #Creates a build directory
  mkdir build
  cd build

  #Download and install Anaconda
  CONDA_INSTALL_PATH="/usr/local/anaconda3-4.2.0"
  wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh
  chmod +x Anaconda3-4.2.0-Linux-x86_64.sh
  ./Anaconda3-4.2.0-Linux-x86_64.sh -b -p $CONDA_INSTALL_PATH

  #Add Anaconda path
  echo "\n #Anaconda paths \n" >> /environment
	echo 'export PATH="'$CONDA_INSTALL_PATH'/bin:$PATH"' >> /environment

  #Loads the environment file
  . /environment

  #Install Tensorflow
  TF_PYTHON_URL="https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.1-cp35-cp35m-linux_x86_64.whl"
  pip install --ignore-installed --upgrade $TF_PYTHON_URL

	#Install Keras
	pip install keras

%runscript
	#Executes with the singularity run command
	#delete this section to use existing docker ENTRYPOINT command


%test
	#Test that script is a success
