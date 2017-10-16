FROM debian
LABEL maintainer=@cmhh
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update --fix-missing && \
    apt-get install -yq --no-install-recommends \
    build-essential git \
    wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

