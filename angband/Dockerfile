# Angband is a free, single-player dungeon exploration roguelike game.
#
# Note: angband_volume is used for storing data, make sure you create it.
#
# Run with:
#
# docker run -ti \
#     --name angband \
#     -h angband \
#     --volumes-from angband_volume \
#     angband


FROM ubuntu:14.04
MAINTAINER Peter Barabas <z0d@notresp.com>

ENV DEBIAN_FRONTEND noninteractive

ADD http://rephial.org/downloads/4.0/angband-4.0.5.tar.gz /tmp/

RUN apt-get update && \
    apt-get install --no-install-recommends -y libncursesw5 locales && \
    locale-gen en_US.UTF-8 && \
    apt-get install -y gcc make libncursesw5-dev automake && \
    cd /tmp && \
    tar xf angband-4.0.5.tar.gz && \
    cd angband-4.0.5 && \
    ./autogen.sh && \
    ./configure --localstatedir=/var && \
    make && \
    make install && \
    cd /tmp && \
    rm -rf angband-4.0.5.tar.gz angband-4.0.5 && \
    apt-get purge -y gcc make libncursesw5-dev automake && \
    apt-get autoremove -y && \
    apt-get clean

RUN useradd --create-home angband

ENV LC_CTYPE en_US.UTF-8

ENV HOME /home/angband

USER angband

RUN mkdir /home/angband/.angband

VOLUME /home/angband/.angband

ENTRYPOINT /usr/local/games/angband

