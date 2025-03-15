FROM mcr.microsoft.com/devcontainers/base:jammy

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential cmake \
    git \
    python3 python3-pip python3-setuptools \
    python3-wheel ninja-build \
    libmicrohttpd-dev \
    libjansson-dev \
    libssl-dev \
    libsofia-sip-ua-dev \
    libglib2.0-dev \
    libopus-dev \
    libogg-dev \
    libcurl4-openssl-dev \
    liblua5.3-dev \
    libconfig-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install meson

RUN git clone https://gitlab.freedesktop.org/libnice/libnice && \
    cd libnice && \
    meson --prefix=/usr build && ninja -C build && sudo ninja -C build install

RUN wget https://github.com/cisco/libsrtp/archive/v2.2.0.tar.gz && \
    tar xfv v2.2.0.tar.gz && \
    cd libsrtp-2.2.0 && \
    ./configure --prefix=/usr --enable-openssl && \
    make shared_library && sudo make install

RUN git clone https://libwebsockets.org/repo/libwebsockets && \
    cd libwebsockets && \
    git checkout v4.3-stable && \
    mkdir build && \
    cd build && \
    cmake -DLWS_MAX_SMP=1 -DLWS_WITHOUT_EXTENSIONS=0 -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_C_FLAGS="-fpic" .. && \
    make && sudo make install
