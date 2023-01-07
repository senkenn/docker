FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
  git \
  zip \
  curl \
  zsh \
  ca-certificates \
  gnupg \
  lsb-release

WORKDIR /root

# zsh
RUN zsh
RUN sed -i.bak "s|$HOME:/bin/bash|$HOME:/bin/zsh|" /etc/passwd

# Powerlevel10k
RUN git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $HOME/.p10k

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
