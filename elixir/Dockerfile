FROM elixir:1.19

WORKDIR /root

# install dependency
RUN export DEBIAN_FRONTEND=noninteractive &&  apt update && apt install -y vim-gtk3 git make openssh-client mariadb-client wget curl tree strace ripgrep net-tools unzip nodejs npm && apt autoremove
RUN wget https://github.com/elixir-lsp/elixir-ls/releases/download/v0.29.3/elixir-ls-v0.29.3.zip -O /tmp/elixir_ls.zip \
    && unzip /tmp/elixir_ls.zip -d /usr/local/bin/elixir-ls \
    && rm /tmp/elixir_ls.zip

# config vim
COPY .vimrc .vimrc
RUN curl -fLo /root/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
RUN yes "" | vim +'PlugInstall --sync' +qall && rm -rf /root/.cache/*

# config elixir specific
RUN cd ~/.vim/plugged/coc.nvim && npm ci && rm -rf /root/.npm/_cacache/*
COPY coc-settings.json .vim/
