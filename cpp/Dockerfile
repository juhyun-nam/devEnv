FROM ubuntu:20.04

RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" TZ="Asia/Seoul" apt-get -y install tzdata
RUN apt-get install -y \
    make \
    python3.9 \
    python3-pip \
    less \
    vim \
    curl \
    git \
    valgrind

WORKDIR /tmp
RUN curl -fsSL -o cmake.sh https://github.com/Kitware/CMake/releases/download/v3.19.6/cmake-3.19.6-Linux-x86_64.sh \
    && sh cmake.sh --prefix=/usr/local --skip-license \
    && cmake --version \
    && rm cmake.sh

ARG LLVM=10
RUN apt-get install -y \
    clang-${LLVM} \
    libclang-${LLVM}-dev \
    llvm-${LLVM}-dev \
    clang-tidy-${LLVM} \
    clang-format-${LLVM}
ENV CC=clang-10
ENV CXX=clang++-10

RUN git clone https://github.com/include-what-you-use/include-what-you-use.git \
    && (cd include-what-you-use && git checkout clang_${LLVM}) \
    && mkdir build \
    && (cd build \
    && cmake -DCMAKE_PREFIX_PATH=/usr/lib/llvm-7 ../include-what-you-use \
    && make install) \
    && rm -drf include-what-you-use \
    && rm -drf build

WORKDIR /root
COPY .clang-format .
COPY .clang-tidy .
RUN pip3 install cpplint

