FROM alpine:3.19.1

ARG VERSION

RUN apk add --no-cache \
    libstdc++\
    libjpeg-turbo-dev

RUN apk add --no-cache --virtual builddeps\
    ca-certificates	\
    cmake	\
    g++ \
    gcc \
    git \
    make \
    wget \
    pigz \
    && wget -q https://github.com/rordenlab/dcm2niix/archive/refs/tags/v$VERSION.tar.gz \
    && tar -xzf v$VERSION.tar.gz \
    && mkdir  /dcm2niix-$VERSION/build/ \
    && cd /dcm2niix-$VERSION/build/ \
    && cmake -DBATCH_VERSION=OFF \
    -DBUILD_DOCS=OFF \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local/ \
    -DINSTALL_DEPENDENCIES=OFF \
    -DUSE_GIT_PROTOCOL=OFF \
    -DUSE_JASPER=OFF \
    -DUSE_JPEGLS=ON \
    -DUSE_OPENJPEG=ON \
    -DUSE_STATIC_RUNTIME=ON \
    -DUSE_TURBOJPEG=ON \
    -DZLIB_IMPLEMENTATION=Cloudflare \
    .. \
    && make \
    && make install \
    && cd / \
    && apk del builddeps \
    && rm -rf /dcm2niix-$VERSION \
    && rm -rf v$VERSION.tar.gz \
    && rm -rf /root/.wget-hsts

ENTRYPOINT ["dcm2niix"]
