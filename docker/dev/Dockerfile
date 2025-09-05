FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo 'Asia/Shanghai' > /etc/timezone && \
    sed -i "s@http://.*archive.ubuntu.com@http://mirrors.tuna.tsinghua.edu.cn@g" /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
    git vim wget tzdata libopencv-dev build-essential curl yasm libtool libssl-dev build-essential graphviz \
    libc6 libc6-dev unzip libnuma1 libnuma-dev libx264-dev sudo openjdk-11-jdk maven gcc-9 g++-9 \
    telnet dnsutils libgl1-mesa-glx libglib2.0-0 python3.10 libpython3.10-dev python3-pip gdb lldb \
    net-tools iputils-ping traceroute nmap tcpdump netcat nethogs \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 100 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 100 \
    && ln -sf /usr/bin/python3.10  /usr/bin/python3 \
    && mkdir /opt/arthas && cd /opt/arthas && curl -O https://arthas.aliyun.com/arthas-boot.jar

RUN proxy="http://10.1.171.214:8118" && export https_proxy=$proxy && export http_proxy=$proxy && export ftp_proxy=$proxy \
    && wget https://github.com/Kitware/CMake/releases/download/v3.24.0/cmake-3.24.0.tar.gz -O /tmp/cmake.tar.gz \
    && tar -xzvf /tmp/cmake.tar.gz -C /tmp \
    && cd /tmp/cmake-3.24.0 \
    && ./bootstrap \
    && make -j$(nproc) \
    && make install

RUN curl -sL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN npm config set registry https://registry.npmmirror.com