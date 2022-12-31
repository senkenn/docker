FROM ubuntu:22.04

RUN apt-get update && apt-get install -y git zip curl zsh

WORKDIR $HOME

# Volta
RUN curl https://get.volta.sh | bash

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install && rm awscliv2.zip

# zsh
RUN zsh
RUN sed -i.bak "s|$HOME:/bin/bash|$HOME:/usr/bin/zsh|" /etc/passwd
