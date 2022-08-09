FROM alpine:3.15

ARG VERSION

RUN apk add --no-cache \
    libstdc++=10.3.1_git20211027-r0 \
    libjpeg-turbo-dev=2.1.2-r0

RUN apk add --no-cache --virtual builddeps\
    ca-certificates=20211220-r0	\
    cmake=3.21.3-r0	\
    g++=10.3.1_git20211027-r0 \
    gcc=10.3.1_git20211027-r0 \
    git=2.34.1-r0 \
    make=4.3-r0 \
    wget=1.21.2-r2 \
    pigz=2.6-r0 \
    && wget -q https://github.com/rordenlab/dcm2niix/archive/refs/tags/v$VERSION.tar.gz \
    && tar -xzf v$VERSION.tar.gz \
    && mkdir  /dcm2niix-$VERSION/build/ \
    && cd /dcm2niix-$VERSION/build/ \
    && cmake -DBATCH_VERSION=OFF \
          -DBUILD_DOCS=OFF \
          -DCMAKE_BUILD_TYPE=Release \
          -DCMAKE_INSTALL_PREFIX=/usr/local/ \
          -DINSTALL_DEPENDENCIES=OFF \
          -DUSE_GIT_PROTOCOL=ON \
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
