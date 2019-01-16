ARG CUDA_VERSION=9.2
FROM nvidia/cuda:$CUDA_VERSION-cudnn7-devel-ubuntu16.04
LABEL maintainer "Matt Johnson <mattjj@google.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
            dh-autoreconf git curl \
            build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev \
            libsqlite3-dev wget llvm libncurses5-dev xz-utils tk-dev \
            libxml2-dev libxmlsec1-dev libffi-dev

RUN git clone https://github.com/nixos/patchelf /tmp/patchelf
WORKDIR /tmp/patchelf
RUN bash bootstrap.sh && ./configure && make && make install && rm -r /tmp/patchelf

WORKDIR /
COPY build_wheel_docker_entrypoint.sh /build_wheel_docker_entrypoint.sh
RUN chmod +x /build_wheel_docker_entrypoint.sh

WORKDIR /build
ENV TEST_TMPDIR /build
ENTRYPOINT ["/build_wheel_docker_entrypoint.sh"]
