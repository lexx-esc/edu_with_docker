FROM lexxesc/edu_platform:latest
WORKDIR /root
RUN apt-get update && apt-get -y install python3.10-venv && /usr/bin/python3 -m venv venv
COPY ./config/ ./
COPY ./jupyter ./.jupyter
RUN cat zshrc_update >> .zshrc && rm zshrc_update 
RUN ./venv/bin/pip3 install -r ./requirement.txt && rm requirement.txt
WORKDIR /root/app
EXPOSE 8888
CMD ["/usr/sbin/sshd", "-D"]
