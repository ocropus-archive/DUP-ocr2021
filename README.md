# Large Scale Processing and Training for OCR, Content Analysis, and Information Extraction

The objective of this tutorial is to introduce students to methods and tools for large-scale training and inference for OCR and content analysis.

- discussion of deep learning for OCR: text recognition, segmentation, preprocessing, table analysis
- different kinds of self-supervised, semi-supervised, and unsupervised training for OCR
- bootstrapping training from unlabeled data
- representation of big OCR datasets using WebDataset, shards, and OCR
- large scale data processing with Docker and Kubernetes

The tutorial will consist of short presentations and hands-on experimentation.

# Setting Up your Machine

The entire runtime, packages, Python installations, and utilities needed
for the tutorial are packaged up in a single Docker image called "tmbdev/ocr2021".
If you have Docker running on your machine, you should be able to run
this image.

**Please set up Docker on your machine before the start of the tutorial so that
you can get started right away.**

Ideally, you should also have a GPU available to you, though you can
run the scripts (albeit slowly) without a GPU.

## Setup on Linux

You may be able to use Docker from your Ubuntu (or other Linux) distro directly using the built-in docker package, though the docker.io package is preferable. Ideally, you also set up your machine to support NVIDIA GPUs.

- [NVIDIA documentation for Docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).
- [Gist showing docker.io and nvidia-docker2 installation](https://gist.github.com/tmbdev/e94fe7f6a98dbfcab164616340f95e81)
- On Ubuntu, you can install Kubernetes with `snap install microk8s`

## Setup on Windows with VirtualBox

You can install Ubuntu on Windows by using the free
[VirtualBox](https://www.virtualbox.org/) software. That software works
on Windows, Linux, and OS X. After installing VirtualBox, you can install
Ubuntu 20.04 directly in it. There is no GPU suppport with this setup, however.

## Setup on Windows with WSL

Instead of VirtualBox, you can use Microsoft WSL to run Unbuntu on
Windows. Microsoft also provides a version of Docker that integrates with
both Windows and WSL and supports Kubernetes. Be sure to install Ubuntu
(20.04) for WSL. GPU computing is supported by WSL and Docker on WSL.

The steps for making this work are: (1) install WSL on Windows,
(2) upgrade to WSL2, (3) install Docker for Windows ([Docker
info](https://docs.docker.com/desktop/windows/install/), [Microsoft
Documentation](https://docs.microsoft.com/en-us/virtualization/windowscontainers/)),
(4) enable Kubernetes in Docker for Windows.
For CUDA support, install NVIDIA drivers for
Windows and NVIDIA drivers for WSL
([CUDA on WSL](https://docs.nvidia.com/cuda/wsl-user-guide/index.html)).

## Setup on OSX

[Here](https://docs.docker.com/desktop/mac/install/) is the guide for
installing Docker on OSX. You need an x86 Mac for this to work. There
does not seem to be CUDA support on OSX.

Installing VirtualBox is another alternative.

## Remote Access to Your Desktop

If you have Linux/Ubuntu installed on your desktop but are working on a laptop,
consider just installing Docker on your desktop and accessing your desktop
remotely via VNC.
