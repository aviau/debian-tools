FROM debian:unstable

RUN bash -c "echo 'deb-src http://ftp.debian.org/debian unstable main' >> /etc/apt/sources.list"

RUN apt-get update && \
    apt-get install -y \
        sudo \
        git \
        gnupg2 \
        vim \
        build-essential \
        cowbuilder \
        quilt \
        git-buildpackage

ARG userid
ARG username

RUN useradd -m -u "$userid" $username
RUN bash -c "echo '$username ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers"

USER $username

WORKDIR /home/aviau
