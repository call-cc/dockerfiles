FROM ubuntu:14.04
MAINTAINER Peter Barabas <z0d@notresp.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y git gcc libc6-dev make

RUN cd /tmp && \
    git clone https://github.com/debrouxl/gcc4ti && \
    cd gcc4ti/trunk/tigcc-linux/scripts && \
    ./updatesrc && \
    cd ../gcc4ti-0.96b11 && \
    yes '' | ./scripts/Install && \
    apt-get purge -y git gcc && \
    apt-get autoremove -y && \
    apt-get clean

RUN useradd --create-home ti

USER ti

WORKDIR /home/ti
ENV HOME /home/ti
ENV PATH=$PATH:/usr/local/share/gcc4ti/bin

RUN mkdir /home/ti/dev

VOLUME /home/ti/dev

CMD /bin/bash

