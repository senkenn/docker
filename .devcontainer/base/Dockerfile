FROM ubuntu:22.04

RUN apt-get update && apt-get install -y git zip

# install zsh
RUN apt-get install -y zsh
RUN zsh
RUN sed -i.bak "s|$HOME:/bin/bash|$HOME:/usr/bin/zsh|" /etc/passwd

# install zsh extension (prezto)
RUN git clone --recursive https://github.com/sorin-ionescu/prezto.git $HOME/.zprezto
RUN ln -s $HOME/.zprezto/runcoms/zlogin    $HOME/.zlogin \
  && ln -s $HOME/.zprezto/runcoms/zlogout   $HOME/.zlogout \
  && ln -s $HOME/.zprezto/runcoms/zpreztorc $HOME/.zpreztorc \
  && ln -s $HOME/.zprezto/runcoms/zprofile  $HOME/.zprofile \
  && ln -s $HOME/.zprezto/runcoms/zshenv    $HOME/.zshenv \
  && ln -s $HOME/.zprezto/runcoms/zshrc     $HOME/.zshrc
RUN echo "zstyle ':prezto:module:prompt' theme 'powerlevel10k'" >> $HOME/.zpreztorc
COPY .p10k.zsh /root
COPY .zshrc /root
SHELL [ "zsh" ]

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install && rm awscliv2.zip
