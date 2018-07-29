FROM ubuntu:latest
MAINTAINER danilonc

WORKDIR /opt

# Install Necessary tools
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get install -y build-essential python-pip cmake python-ipython git ipython time vim

# Download capstone, keystone and unicorn source-code

RUN git clone https://github.com/keystone-engine/keystone.git
RUN git clone https://github.com/aquynh/capstone.git
RUN git clone https://github.com/unicorn-engine/unicorn.git

# Build Capstone
WORKDIR /opt/capstone
RUN git checkout tags/3.0.5
RUN ./make.sh && ./make.sh install

# Build Keystone
WORKDIR /opt/keystone
RUN git checkout tags/0.9.1
RUN mkdir build
WORKDIR /opt/keystone/build
RUN ../make-lib.sh && make install
RUN ../make-share.sh && make install

# Build unicorn
WORKDIR /opt/unicorn
RUN git checkout tags/1.0.1
RUN mkdir build
RUN ./make.sh && ./make.sh install 

# ldconfig new libraries
RUN ldconfig

# Install python keybinds
RUN pip install --upgrade keystone-engine capstone unicorn