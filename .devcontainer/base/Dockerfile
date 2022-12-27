FROM ubuntu:22.04

RUN apt-get update && apt-get install -y git

# Install Docker
RUN apt-get install -y \
  ca-certificates \
  curl \
  gnupg \
  lsb-release
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

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

# SSHの鍵を設定
RUN mkdir $HOME/.ssh
RUN echo 'Host github.com' >> $HOME/.ssh/config \
  && echo '  HostName github.com' >> $HOME/.ssh/config \
  && echo '  User git' >> $HOME/.ssh/config \
  && echo '  IdentityFile ~/.ssh/id_rsa' >> $HOME/.ssh/config \
  && echo '  IdentitiesOnly yes' >> $HOME/.ssh/config
