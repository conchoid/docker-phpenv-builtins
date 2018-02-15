FROM conchoid/docker-phpenv:v1-1-5.6-alpine3.6

ENV PHP_CONFIGURE_OPTS "--disable-fpm --disable-cgi"
ENV PREINSTALLED_VERSIONS "\
5.3.29\n\
5.4.45\n\
5.5.38\n\
5.6.33\n\
7.0.27\n\
7.1.13\n\
7.2.1"

RUN set -x \
    && export CONFIGURE_OPTS="$PHP_CONFIGURE_OPTS" \
    && export CFLAGS="$PHP_CFLAGS" \
    && echo -e "$PREINSTALLED_VERSIONS" | while read version;do \
         phpenv install $version; done \
    && rm -rf "/tmp/php-build*"
