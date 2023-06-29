#### tgi适配gpu机型
```

FlashAttention currently supports:

1.  Turing, Ampere, Ada, or Hopper GPUs (e.g., H100, A100, RTX 3090, T4, RTX 2080).
2.  fp16 and bf16 (bf16 requires Ampere, Ada, or Hopper GPUs).
3.  Had dimensions that are multiples of 8, up to 128 (e.g., 8, 16, 24, ..., 128). Head dim > 64 backward requires A100 or H100.
```

#### 使用问题
```bash
1、安装docker
sudo dnf install -y tar bzip2 make automake gcc gcc-c++ vim pciutils elfutils-libelf-devel libglvnd-devel iptables

sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

sudo dnf repolist -v

sudo dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.4.3-3.1.el7.x86_64.rpm

sudo dnf install docker-ce -y

sudo systemctl --now enable docker

sudo docker run --rm hello-world

2、docker中安装nvidia驱动

distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.repo | sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo

sudo dnf clean expire-cache --refresh

curl https://nvidia.github.io/nvidia-docker/centos8/nvidia-docker.repo > /etc/yum.repos.d/nvidia-docker.repo

sudo dnf install -y nvidia-container-toolkit

sudo nvidia-ctk runtime configure --runtime=docker

sudo systemctl restart docker

sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:11.6.2-base-ubuntu20.04 nvidia-smi
```
