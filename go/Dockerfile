FROM ubuntu:20.04

RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" TZ="Asia/Seoul" apt-get -y install tzdata
RUN apt-get install -y \
    make \
    less \
    vim \
    curl \
    git

WORKDIR /tmp
RUN curl -o go1.16.linux-amd64.tar.gz -fsSL https://golang.org/dl/go1.16.linux-amd64.tar.gz \
    && rm -rf /usr/local/go \
    && tar -C /usr/local -xzf go1.16.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin

RUN curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b /usr/local/go/bin v1.37.1

WORKDIR /root
COPY .golangci.yml .
