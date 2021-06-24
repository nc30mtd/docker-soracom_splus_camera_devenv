FROM ubuntu:18.04
MAINTAINER mtd <mtd@mtdfab.jp>

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        wget \
        libssl-dev \
        libbz2-dev \
        libreadline-dev \
        libsqlite3-dev \
        git \
        zlib1g-dev \
        libffi-dev \
        ca-certificates 
        # python3 \
        # python3-pip \
        # python3-venv

RUN apt-get install python3-pip
RUN pip3 install cmake
RUN apt-get install libwebp*
RUN apt-get install libsm6 libxrender1 libxext-dev

# pyenvの環境を構築
WORKDIR /root
ENV HOME /root
RUN git clone https://github.com/yyuu/pyenv.git $HOME/.pyenv
ENV PYENV_ROOT $HOME/.pyenv
RUN echo $PYENV_ROOT
ENV PATH $PYENV_ROOT/bin:$PATH
RUN echo $PATH
RUN eval "$(pyenv init -)"

# python 3.7.3をインストール
RUN pyenv install 3.7.3
RUN pyenv local 3.7.3
RUN pyenv rehash

# # venvの環境を構築
# # RUN mkdir -p /opt/soracom/python/
# # ENV self $(whoami)
# # RUN chown -R $self /opt/soracom/
# # RUN python -m venv /opt/soracom/python/
# # RUN source /opt/soracom/python/bin/activate

# RUN mkdir -p /opt/soracom/python/
# RUN chown -R root:root /opt/soracom/
# RUN python3 -m venv /opt/soracom/python/
# RUN echo "source /opt/soracom/python/bin/activate" >> /root/.bashrc