FROM alpine:latest

RUN apk update \
    && apk upgrade \
    && mkdir -p /etc/apk \
    # && echo "http://alpine.gliderlabs.com/alpine/edge/main" >> /etc/apk/repositories \
    # && echo "http://alpine.gliderlabs.com/alpine/edge/community" >> /etc/apk/repositories \
    && apk add --update tzdata \
    && cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    && apk add --no-cache --virtual --update \
    php5 \ 
    php5-apcu \ 
    php5-bcmath \ 
    php5-bz2 \
    php5-cli \
    php5-ctype \ 
    php5-curl \ 
    php5-dom \
    php5-exif \
    php5-gd \
    php5-gettext \ 
    php5-iconv \ 
    php5-intl \ 
    php5-json \ 
    php5-mcrypt \
    php5-memcache \
    php5-mysql \
    php5-mysqli \ 
    php5-openssl \ 
    php5-pcntl \ 
    php5-pdo_mysql \ 
    php5-pdo_pgsql \ 
    php5-pdo_sqlite \ 
    php5-phar \ 
    php5-posix \ 
    php5-soap \
    php5-xcache \
    php5-xmlreader \ 
    php5-xmlrpc \
    php5-xsl \
    php5-zip \
    php5-zlib \
    ca-certificates \
    openssh \
    && echo "${TINI_SHA} /sbin/tini" | sha1sum -wc - \
    && sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php5/php.ini \
    && sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php5/php.ini \
    && sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php5/php.ini \
    && sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php5/php.ini \
    && sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php5/php.ini \

    # Clean up

    && apk del tzdata \
    && rm -rf /var/cache/apk/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* 