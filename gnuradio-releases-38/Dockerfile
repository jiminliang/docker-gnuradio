FROM ubuntu:20.04
LABEL maintainer="Federico 'Larroca' La rocca - flarroca@fing.edu.uy"

# change the source

RUN sed -i 's@http://archive.ubuntu.com/ubuntu/@http://mirrors.aliyun.com/ubuntu/@g' /etc/apt/sources.list

#ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update

# else it will output an error about Gtk namespace not found
RUN apt-get install -y gir1.2-gtk-3.0

# to have add-apt-repository available
RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:gnuradio/gnuradio-releases-3.8

# create user gnuario38 with sudo (and password genetic00)
RUN apt-get install -y sudo
RUN useradd --create-home --shell /bin/bash -G sudo gnuradio38
RUN echo 'gnuradio38:genetic00' | chpasswd

# I create a dir at home which I'll use to persist after the container is closed (need to change it's ownership)
RUN mkdir /home/gnuradio38/persistent38  && chown gnuradio38 /home/gnuradio38/persistent38

RUN apt-get update

RUN apt-get install -y gnuradio

# installing other packages needed for downloading and installing OOT modules
RUN apt-get install -y gnuradio-dev cmake git libboost-all-dev libcppunit-dev liblog4cpp5-dev swig liborc-dev libgsl-dev

# of course, nothing useful can be done without vim
RUN apt-get install -y vim 

USER gnuradio38

WORKDIR /home/gnuradio38

ENV PYTHONPATH "${PYTHONPATH}:/usr/local/lib/python3/dist-packages"

CMD bash
