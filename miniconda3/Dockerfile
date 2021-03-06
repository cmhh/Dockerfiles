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

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet \
      https://repo.continuum.io/miniconda/Miniconda3-4.3.11-Linux-x86_64.sh -O ~/miniconda.sh && \
      /bin/bash ~/miniconda.sh -b -p /opt/conda && \
      rm ~/miniconda.sh

RUN apt-get update --fix-missing && \
  apt-get install -y curl grep sed dpkg && \
  apt-get clean
  
RUN TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
  curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
  dpkg -i tini.deb && \
  rm tini.deb
  
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

ENTRYPOINT [ "/usr/bin/tini", "--"]