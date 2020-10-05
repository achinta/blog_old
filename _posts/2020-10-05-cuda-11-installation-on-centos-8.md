Here I will describe the steps I followed to install cuda 11.1 on a fresh Centos 8 server. This involves three steps. 

### 1. Installing Nvidia driver
. 
```shell
# Install development tools which include gcc and make
sudo dnf group install "Development Tools"
sudo yum install elfutils-libelf-devel

# install libelf
yum install elfutils-libelf-devel

# install dkms
sudo yum install epel-release -y
sudo yum install dkms -y

# install the driver
sudo bash NVIDIA-Linux-x86_64-450.80.02.run
```
### 2. Install cuda
Download cuda from https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=CentOS&target_version=8&target_type=rpmlocal
Follow the commands given on the page. 
For me, it was
```shell
wget https://developer.download.nvidia.com/compute/cuda/11.1.0/local_installers/cuda-repo-rhel8-11-1-local-11.1.0_455.23.05-1.x86_64.rpm
sudo rpm -i cuda-repo-rhel8-11-1-local-11.1.0_455.23.05-1.x86_64.rpm
sudo dnf clean all
sudo dnf -y module install nvidia-driver:latest-dkms
sudo dnf -y install cuda

# verify the cuda version
nvidia-smi
```

### 3. Install cudnn
To download cudnn, we need to login to nvidia website, which is not possible on the server. So I did it locally and copied the files to server. 
```shell
sudo rpm -ivh libcudnn8-8.0.4.30-1.cuda11.1.x86_64.rpm
sudo rpm -ivh libcudnn8-devel-8.0.4.30-1.cuda11.1.x86_64.rpm
```
