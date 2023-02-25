FROM python:3.7.16

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# DOCKER_USER for the Docker user
ARG username=vscode
ARG useruid=1000
ARG usergid=${useruid}

# install package
RUN apt-get -y update && apt-get upgrade -qqy && apt-get -y install \
    bash \
    curl \
    gcc \
    git \
    jq \
    sudo \
    build-essential \
    g++ \
    make \
    cmake \
    libtool \
    texinfo \
    dpkg-dev \
    pkg-config \
    gfortran \
    libopenblas-dev \
    swig

# install faiss
RUN pip install --upgrade pip && \
    pip install numpy faiss-cpu

# create group and user
RUN groupadd --gid ${usergid} ${username} && \
    useradd -s /bin/bash --uid ${useruid} --gid ${usergid} -m ${username} && \
    gpasswd -a ${username} sudo

# Import profile for bash
COPY bash_profile /home/${username}/.bash_profile
RUN chown ${username}:${username} /home/${username}/.bash_profile

# switch to user
USER ${username}
