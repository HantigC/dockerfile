ARG BASE_IMAGE=ubuntu:18.04
FROM ${BASE_IMAGE}

ARG USER_ID=1000
ARG GROUP_ID=1000
ARG USERNAME="hsc"
ARG NVIM_VERSION="v0.8.3"
ARG NVIM_LINK="https://github.com/neovim/neovim/releases/download/${NVIM_VERSION}/nvim-linux64.deb"

ENV DEBIAN_FRONTEND=noninteractive




RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    sudo \
    build-essential \
    software-properties-common \
    ca-certificates \
    bzip2 \
    git \
    make \
    ripgrep \
    fd-find \
    automake \
    cmake \
    g++ \
    pkg-config \
    unzip \
    wget \
    curl


RUN groupadd -g $GROUP_ID ${USERNAME} && \
    useradd -r -u $USER_ID -g $GROUP_ID -m ${USERNAME} && \
    usermod -aG sudo ${USERNAME} && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

WORKDIR /tmp/neovim
RUN wget -O /tmp/nvim.deb ${NVIM_LINK} \
    && apt install /tmp/nvim.deb


USER ${USERNAME}

RUN git clone --bare https://github.com/HantigC/dotfiles.git ${HOME}/.dotfiles \
    && git --git-dir=${HOME}/.dotfiles --work-tree=${HOME} checkout

CMD ["bash"]
