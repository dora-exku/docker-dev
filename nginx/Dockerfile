FROM ubuntu:22.10

ENV NGINX_VERSION 1.23.3
ENV INSTALL_PATH /usr/local
ENV PATH ${INSTALL_PATH}/nginx/sbin:${PATH}

RUN adduser --system --group www

RUN apt-get update \
    && apt-get -y install wget curl \
    && apt-get -y install gcc make \
    && apt-get -y install openssl libssl-dev \
    && apt-get -y install libpcre3 libpcre3-dev \
    && apt-get -y install zlib1g-dev \
    && apt-get -y install libgd-dev

RUN wget https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && tar -xvf nginx-${NGINX_VERSION}.tar.gz \
    && cd nginx-${NGINX_VERSION} \
    && ./configure \
    --user=www \
    --group=www \
    --with-http_ssl_module \
    --with-http_dav_module \
    --with-http_v2_module \
    --with-stream \
    --with-stream_ssl_module \
    --with-stream_ssl_preread_module \
    --with-http_stub_status_module \
    --with-http_ssl_module \
    --with-http_image_filter_module \
    --with-http_gzip_static_module \
    --with-http_gunzip_module \
    --with-http_sub_module \
    --with-http_flv_module \
    --with-http_addition_module \
    --with-http_realip_module \
    && make \
    && make install

RUN mkdir ${INSTALL_PATH}/nginx/conf/sites

COPY nginx.conf /usr/local/nginx/conf/nginx.conf

ENTRYPOINT ["/usr/local/nginx/sbin/nginx"]

CMD ["-g", "daemon off;"]

EXPOSE 80
EXPOSE 443