FROM ubuntu:20.04
LABEL maintainer="Federico 'Larroca' La rocca - flarroca@fing.edu.uy"

ENV DEBIAN_FRONTEND=noninteractive

# change the source

RUN sed -i 's@http://archive.ubuntu.com/ubuntu/@http://mirrors.aliyun.com/ubuntu/@g' /etc/apt/sources.list

RUN apt-get update

# else it will output an error about Gtk namespace not found
RUN apt-get install -y gir1.2-gtk-3.0

# to have add-apt-repository available
RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:gnuradio/gnuradio-releases

# create user gnuario310 with sudo (and password genetic00)
RUN apt-get install -y sudo
RUN useradd --create-home --shell /bin/bash -G sudo gnuradio310
RUN echo 'gnuradio310:genetic00' | chpasswd

# I create a dir at home which I'll use to persist after the container is closed (need to change it's ownership)
RUN mkdir /home/gnuradio310/persistent310  && chown gnuradio310 /home/gnuradio310/persistent310

RUN apt-get update

RUN apt-get install -y gnuradio

# installing other packages needed for downloading and installing OOT modules
RUN apt-get install -y gnuradio-dev cmake git libboost-all-dev libcppunit-dev liblog4cpp5-dev python3-pygccxml pybind11-dev liborc-dev python3-pip libgsl-dev

# of course, nothing useful can be done without vim
RUN apt-get install -y vim 

# Fix dependency issue as noted on 'InstallingGR' wiki page for 3.10
RUN pip install packaging

USER gnuradio310

WORKDIR /home/gnuradio310

ENV PYTHONPATH "${PYTHONPATH}:/usr/local/lib/python3/dist-packages"

CMD bash
