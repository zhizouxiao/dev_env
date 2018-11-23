FROM centos:latest

RUN yum -y upgrade

# install vim
RUN curl -L https://copr.fedorainfracloud.org/coprs/unixcommunity/vim/repo/epel-7/unixcommunity-vim-epel-7.repo -o /etc/yum.repos.d/unixcommunity-vim-epel-7.repo
RUN yum -y update vim*

# install git, zsh
RUN yum -y install git, zsh, go

# ag

# add user
RUN groupadd -r worker && useradd -r -g worker worker && su worker

# zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

RUN gosu chsh -s /bin/zsh

# vim plugin
RUN git clone --depth=1 https://github.com/amix/vimrc.git ~/.vim_runtime &&
sh ~/.vim_runtime/install_awesome_vimrc.sh

