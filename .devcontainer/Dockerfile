FROM ubuntu:24.04

# install common utils
RUN apt-get update && apt-get install -y \
    locales \
    git \
    sudo \
    tree

# locale settings for japanese
ENV TZ=Asia/Tokyo
ENV LANG=ja_JP.UTF-8
RUN sed -i -e 's/# \(ja_JP.UTF-8\)/\1/' /etc/locale.gen &&\
    locale-gen &&\
    update-locale

# user settings
ARG USERNAME=ubuntu
RUN usermod -aG sudo $USERNAME &&\
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME &&\
    chmod 0440 /etc/sudoers.d/$USERNAME
USER $USERNAME
ENV HOME=/home/$USERNAME
WORKDIR $HOME

# flutter setup
ARG FLUTTER_VERSION=3.35.6
RUN git clone -b $FLUTTER_VERSION https://github.com/flutter/flutter.git
ENV FLUTTER_HOME=$HOME/flutter
ENV PATH="$FLUTTER_HOME/bin:${PATH}"

# apt-get cleanup
RUN sudo apt-get clean -y &&\
    sudo rm -rf /var/lib/apt/lists/*