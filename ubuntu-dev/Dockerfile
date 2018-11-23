FROM ubuntu:latest
# FROM golang:1.11

RUN apt-get update

# install git, zsh, ag, curl
RUN apt-get -y install git zsh silversearcher-ag curl python software-properties-common
RUN apt-get install -y sudo && rm -rf /var/lib/apt/lists/*

RUN add-apt-repository ppa:jonathonf/vim && apt update && apt install -y vim

COPY go1.11.2.linux-amd64.tar.gz /tmp/go1.11.2.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf /tmp/go1.11.2.linux-amd64.tar.gz

# add user
RUN useradd -ms /bin/bash worker && echo "worker:worker" | chpasswd && adduser worker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER worker
WORKDIR /home/worker

# zsh
RUN git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

RUN sudo chsh -s /bin/zsh

# vim plugin
RUN git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime && sh ~/.vim_runtime/install_awesome_vimrc.sh

RUN mkdir -p ~/gocode/src ~/gocode/bin

COPY .zshrc /home/worker/.zshrc

ENTRYPOINT ["zsh"]
