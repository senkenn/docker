FROM ubuntu:22.04

ARG WORKDIR

RUN apt-get update && apt-get install -y \
  git \
  vim \
  zip \
  curl \
  zsh \
  ca-certificates \
  gnupg \
  lsb-release

WORKDIR $HOME

# zsh
RUN zsh
RUN sed -i.bak "s|$HOME:/bin/bash|$HOME:/bin/zsh|" /etc/passwd

# install zsh extension (prezto)
RUN git clone --recursive https://github.com/sorin-ionescu/prezto.git $HOME/.zprezto
RUN ln -s $HOME/.zprezto/runcoms/zlogin    $HOME/.zlogin \
  && ln -s $HOME/.zprezto/runcoms/zlogout   $HOME/.zlogout \
  && ln -s $HOME/.zprezto/runcoms/zpreztorc $HOME/.zpreztorc \
  && ln -s $HOME/.zprezto/runcoms/zprofile  $HOME/.zprofile \
  && ln -s $HOME/.zprezto/runcoms/zshenv    $HOME/.zshenv
RUN echo "zstyle ':prezto:module:prompt' theme 'powerlevel10k'" >> $HOME/.zpreztorc

RUN echo 'Host github.com' >> $HOME/.ssh/config \
  && echo '  HostName github.com' >> $HOME/.ssh/config \
  && echo '  User git' >> $HOME/.ssh/config \
  && echo '  IdentitiesOnly true' >> $HOME/.ssh/config

# Volta
RUN curl https://get.volta.sh | bash

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install && rm awscliv2.zip

# Docker -> https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

WORKDIR $WORKDIR
