FROM ubuntu:14.04
MAINTAINER Peter Barabas <z0d@notresp.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y pkg-config libltdl7-dev libgmp10 libgmp-dev libunistring-dev libffi-dev libgc-dev make libreadline6-dev libgc1c2 libunistring0

ADD http://ftp.gnu.org/gnu/guile/guile-2.0.11.tar.gz /tmp/

RUN cd /tmp && \
    tar xzf guile-2.0.11.tar.gz && \
    cd guile-2.0.11 && \
    ./configure --prefix=/usr/local && \
    make && make install && \
    cd /tmp && \
    rm -rf guile-2.0.11 guile-2.0.11.tar.gz && \
    apt-get purge -y libltdl7-dev libgmp-dev libunistring-dev libffi-dev libgc-dev make libreadline6-dev autotools-dev cpp cpp-4.8 gcc gcc-4.8 manpages manpages-dev && \
    apt-get autoremove -y && \
    apt-get clean

RUN useradd --create-home guile

USER guile

WORKDIR /home/guile
ENV HOME /home/guile
ENV LD_LIBRARY_PATH=/usr/local/lib

RUN mkdir /home/guile/dev

VOLUME /home/guile/dev

CMD /usr/local/bin/guile

