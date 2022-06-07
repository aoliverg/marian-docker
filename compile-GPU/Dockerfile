FROM nvidia/cuda:11.4.0-devel-ubuntu20.04
#you may want to change the cuda version depending on your computer. For example:
#FROM nvidia/cuda:11.6.0-devel-ubuntu20.04

MAINTAINER Antoni Oliver <aoliverg@uoc.edu>
LABEL description="marian compiled."

# Install necessary system packages 
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -yq && apt-get install -yq \
                build-essential \
                git-core \
                pkg-config \
                libtool \
                zlib1g-dev \
                libbz2-dev \
                automake \
                python3-dev \
                perl \
                libsparsehash-dev \
                libboost-all-dev \
                libprotobuf17 \
                protobuf-compiler \
                libprotobuf-dev \ 
                openssl \ 
                libssl-dev \ 
                libgoogle-perftools-dev \
                wget \
                apt-transport-https ca-certificates gnupg software-properties-common \
                cmake \
                vim nano unzip gzip python3-pip php \
                nvidia-utils-470 \
            && rm -rf /var/lib/apt/lists/*
            



WORKDIR /root
# Install Marian


#clone the development version
#RUN git clone https://github.com/marian-nmt/marian-dev
#ENV MARIANPATH /root/marian-dev

#you may want to clone the latest stable verion
RUN git clone https://github.com/marian-nmt/marian
ENV MARIANPATH /root/marian


WORKDIR $MARIANPATH
RUN mkdir -p build
WORKDIR $MARIANPATH/build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release -DUSE_STATIC_LIBS=on -DCOMPILE_SERVER=on -DUSE_SENTENCEPIECE=ON && make -j4

WORKDIR /root


RUN mkdir marian-bin
RUN cp $MARIANPATH/build/marian* ./marian-bin
RUN cp $MARIANPATH/build/spm* ./marian-bin
RUN rm -rf $MARIANPATH
