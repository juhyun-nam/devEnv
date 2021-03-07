FROM ubuntu:20.04

RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" TZ="Asia/Seoul" apt-get -y install tzdata
RUN apt-get install -y \
    make \
    python3.9 \
    python3-pip \
    python3-venv \
    less \
    vim \
    curl \
    git

WORKDIR /root
RUN python3 -m venv /opt/venv
RUN pip3 install \
    flake8 \
    black \
    isort \
    yapf \
    pylint \
    pyre-check

COPY setup.cfg .
COPY pylintrc .
COPY Makefile .

RUN echo ". /opt/venv/bin/activate" >> .bashrc
