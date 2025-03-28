FROM mcr.microsoft.com/devcontainers/base:debian

ARG USER=vscode

# Install linux dependencies
RUN apt-get update &&\
    apt-get install -y clang cmake ninja-build pkg-config libgtk-3-dev &&\
    # For https://pub.dev/packages/flutter_secure_storage_linux
    apt-get install -y libsecret-1-dev libjsoncpp-dev &&\
    apt dist-upgrade -y

# Get latest Flutter
ENV FLUTTER_HOME=/usr/bin/flutter
RUN mkdir -p $FLUTTER_HOME &&\
    git clone -b stable https://github.com/flutter/flutter $FLUTTER_HOME
ENV PATH="${FLUTTER_HOME}/bin:${PATH}"
RUN chmod +x $FLUTTER_HOME/bin/flutter &&\
    git config --global --add safe.directory '*' &&\
    flutter precache

# Install flutter bash completion
RUN chown 1000:1000 $FLUTTER_HOME -R
USER ${USER}

# Source flutter bash completion
RUN echo 'source <(flutter bash-completion)' >> ~/.bashrc &&\
    flutter doctor
