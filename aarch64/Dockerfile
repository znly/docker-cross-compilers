FROM debian:testing
MAINTAINER Steeve Morin "steeve@zen.ly"

# Add the cross compiler sources
RUN apt-get update && apt-get install -y curl gnupg && \
    echo "deb http://emdebian.org/tools/debian/ unstable main" > /etc/apt/sources.list.d/crosstools.list && \
    dpkg --add-architecture arm64 && \
    curl -L http://emdebian.org/tools/debian/emdebian-toolchain-archive.key | apt-key add -

RUN apt-get update && apt-get -y install \
                        build-essential \
                        gcc-6-aarch64-linux-gnu \
                        g++-6-aarch64-linux-gnu

ENV CROSS_TRIPLE aarch64-linux-gnu
ENV CROSS_ROOT /usr/${CROSS_TRIPLE}
ENV PATH ${PATH}:${CROSS_ROOT}/bin
ENV LD_LIBRARY_PATH ${CROSS_ROOT}/lib:${LD_LIBRARY_PATH}

RUN cd /usr/bin && \
    ln -s ${CROSS_TRIPLE}-gcc-6 ${CROSS_TRIPLE}-gcc && \
    ln -s ${CROSS_TRIPLE}-gcc-6 ${CROSS_TRIPLE}-cc && \
    ln -s ${CROSS_TRIPLE}-g++-6 ${CROSS_TRIPLE}-g++ && \
    ln -s ${CROSS_TRIPLE}-g++-6 ${CROSS_TRIPLE}-c++
