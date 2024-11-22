FROM ubuntu:24.04

WORKDIR /root

# install dependency
RUN apt update && export DEBIAN_FRONTEND=noninteractive  && apt install -y vim golang-1.23  git make openssh-client mariadb-client wget curl tree strace ripgrep net-tools unzip nodejs npm && apt autoremove
ENV PATH /lib/go-1.23/bin:/root/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN ln -sf /lib/go-1.23/bin/go /usr/bin

# config vim
COPY .vimrc .vimrc
RUN curl -fLo /root/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
RUN yes "" | vim +'PlugInstall --sync' +qall && rm -rf /root/.cache/*

# config golang specific
RUN cd ~/.vim/plugged/coc.nvim && npm ci && rm -rf /root/.npm/_cacache/*
COPY coc-settings.json .vim/
