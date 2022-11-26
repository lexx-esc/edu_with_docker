FROM ubuntu:22.04
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y language-pack-ru
ENV LANGUAGE ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
RUN locale-gen ru_RU.UTF-8 && dpkg-reconfigure locales
RUN apt-get update && apt-get install -y openssh-server openssh-client zsh vim git && chsh -s /bin/zsh && /usr/bin/ssh-keygen -A && mkdir /run/sshd
RUN echo 'PermitRootLogin yes\nPasswordAuthentication yes\nPermitEmptyPasswords yes' >> /etc/ssh/sshd_config
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.3/zsh-in-docker.sh)" -- \
    -t robbyrussell \
    -p https://github.com/zsh-users/zsh-autosuggestions 
ENV ZSH_AUTOSUGGEST_HILIGHT_STYLE = "fg=#dedede, #bg=9c9c9c, bold, underline"
EXPOSE 22
WORKDIR /root/app