FROM ubuntu:22.04
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y language-pack-ru
ENV LANGUAGE ru_RU.UTF-8
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
RUN locale-gen ru_RU.UTF-8 && dpkg-reconfigure locales
RUN apt-get install -y openssh-server openssh-client zsh vim git && chsh -s /bin/zsh && /usr/bin/ssh-keygen -A && mkdir /run/sshd
RUN echo 'PermitRootLogin yes\nPasswordAuthentication yes\nPermitEmptyPasswords yes' >> /etc/ssh/sshd_config
EXPOSE 22
WORKDIR /root/app
COPY ./configs /root
