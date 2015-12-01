FROM debian

COPY patch /patch

RUN apt-get -y update \
    && apt-get -y install wget build-essential bison \
    && mkdir /usr/local/src/bash \
    && wget -qO- http://ftp.gnu.org/gnu/bash/bash-2.05b.tar.gz | tar zx -C /usr/local/src/bash --strip-components=1 \
    && cd /usr/local/src/bash \
    && wget -qO- $(seq -f "http://ftp.gnu.org/gnu/bash/bash-2.05b-patches/bash205b-%03g" 13) | patch -p0 \
    && patch -p0 -i /patch \
    && ./configure \
    && make \
    && make install \
    && rm -rf /usr/local/src/bash \
    && rm /bin/bash \
    && ln -s /usr/local/bin/bash /bin/bash \
    && apt-get purge -y --auto-remove wget build-essential bison
