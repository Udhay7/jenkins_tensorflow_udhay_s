# Jenkins

Create two VMs, one master, one slave. Follow this guide to set them up:

https://wiki.jenkins.io/pages/viewpage.action?pageId=75893612

Ensure to label the slave with `tensorflow`, then in your builds you can pass them to the tensorflow agent with the tensorflow label.

If in doubt, check the jenkins set up in AWS. (bring them online as they are currently switched off)

See [Jenkinsfile](Jenkinsfile) for a simple example of how to label a job to a particular executor/agent.

Then on the slave set up tensorflow:

# Tensorflow

OS: Ubuntu 14.04 or 16.04 LTS

Approaches

- Docker (recommended)
- Virtualenv and pip (recommended)
- Pip

## Docker

```
docker run -it -p 8888:8888 tensorflow/tensorflow
```

## VirtualEnv and Pip

```
python3 -m venv tensorflow
source tensorflow/bin/activate
pip install tensorflow
```

## Pip

```
pip install tensorflow
```

## GPU

If a gpu is available, then tensorflow can run on the GPU. If your running in a
VM, passthrough the gpu container by its pci address to the VM.

### Install GPU drivers and Cuda Toolbox

```
sudo apt-get install openjdk-8-jdk git python-dev python3-dev python-numpy python3-numpy build-essential python-pip python3-pip python-virtualenv swig python-wheel libcurl3-dev curl   
curl -O http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo dpkg -i ./cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda-9-0  
```

### Install Cuda Neural Network

Log in here:

https://developer.nvidia.com/cudnn

Download:

cudnn-9.0-linux.tar.gz

And

```
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

Add to .bashrc:

```
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"
export CUDA_HOME=/usr/local/cuda
export PATH="$PATH:/usr/local/cuda/bin"
```

```
pip install tensorflow
```
