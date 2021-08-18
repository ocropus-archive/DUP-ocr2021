# Setting Up your Machine

For the tutorial, you need a running version of docker. Ideally, you should also have a GPU available to you, though you can run the scripts (albeit slowly) without a GPU.

## Setup on Linux

There is a lot of documentation on how to set up Docker and the NVIDIA Docker runtime on Linux, for example [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).

Here is a rough set of steps to set up Docker on your machine.

```Shell
# remove old docker installation if any
apt-get remove -qqy --purge 'docker-*'
apt-get remove -qqy --purge 'docker.*'
# prelims
apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
# add docker key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
# adding docker repo
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
# update
apt-get update
# install docker
apt-get install -qqy docker-ce docker-ce-cli containerd.io
# make sure that you are in group "docker"
sudo usermod -aG docker `whoami`
# log out and back in again to pick up the new group
```

If you also want to use NVIDIA GPUs inside Docker, you need the following as well:


```Shell
# add nvidia docker distro
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
&& curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
&& curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
# update
apt-get update
# install nvidia-docker2
apt-get install -qqy nvidia-docker2
# restart docker
systemctl restart docker
# run test container
docker run --rm --gpus all nvidia/cuda nvidia-smi
```

## Setup on Windows

Running the examples on Windows 10 (e.g., a Windows laptop) requires a number of installs:

- WSL 2 (Windows Subsystem for Linux)
- Docker for Windows

Be sure to install Ubuntu (20.04) for WSL.  Although the bulk of the
code runs inside a Docker container, we will still be using Linux for
scripting. Also be sure to enable WSL integration for Docker so that the "docker" command works from within Ubuntu running under WSL.

If you also want to run CUDA:

- NVIDIA Windows drivers (you probably already have those)
- NVIDIA WSL drivers (you need to install those)
- nvidia-docker2 runtime (just like on Linux)

Here are some links to get you started:

- [Official Docker documentation](https://docs.docker.com/desktop/windows/install/)
- [Microsoft Documentation](https://docs.microsoft.com/en-us/virtualization/windowscontainers/)
- [CUDA on WSL](https://docs.nvidia.com/cuda/wsl-user-guide/index.html)



## Setup on OSX

[Here](https://docs.docker.com/desktop/mac/install/) is the guide for installing Docker on OSX. You need an x86 Mac for this to work. There does not seem to be CUDA support on OSX.