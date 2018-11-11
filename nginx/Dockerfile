FROM ubuntu:18.04
RUN apt-get update \
    && apt-get install -y --no-install-recommends libpcre3-dev make build-essential curl zlib1g-dev ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && cd /tmp \
    && curl http://nginx.org/download/nginx-1.15.6.tar.gz -o nginx.tar.gz \
    && mkdir nginx && tar -xzv -C nginx --strip-components=1 -f nginx.tar.gz \
    && curl https://www.openssl.org/source/openssl-1.1.1.tar.gz -o openssl.tar.gz \
    && mkdir openssl && tar -xzv -C openssl --strip-components=1 -f openssl.tar.gz \
    && curl -L https://github.com/openresty/headers-more-nginx-module/archive/v0.33.tar.gz -o headers-more-nginx-module.tar.gz \
    && mkdir headers-more-nginx-module && tar -xzv -C headers-more-nginx-module --strip-components=1 -f headers-more-nginx-module.tar.gz \
    && cd nginx \
    && sed -i 's/<center>nginx<\/center>//' $(grep "<center>nginx" -rl .) \
    && ./configure --with-pcre-jit --with-stream --with-stream_ssl_module --with-stream_ssl_preread_module --with-http_v2_module --without-mail_pop3_module --without-mail_imap_module --without-mail_smtp_module --with-http_stub_status_module --with-http_realip_module --with-http_addition_module --with-http_gzip_static_module --with-http_sub_module  --with-http_gunzip_module --with-threads --with-stream --with-stream_ssl_module --with-http_ssl_module --with-stream_ssl_preread_module --with-openssl=../openssl --add-module=../headers-more-nginx-module \
    && make \
    && make install \
    && rm -rf /tmp/* \
    && apt-get remove --purge --autoremove -y libpcre3-dev make build-essential curl zlib1g-dev ca-certificates
ENV PATH="/usr/local/nginx/sbin:$PATH"
