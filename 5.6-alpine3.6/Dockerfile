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
    && system_php="/usr/bin/php" \
    && system_php_ver="5.6.33" \
    && version_dir="${PHPENV_ROOT}/versions/${system_php_ver}/bin" \
    && mkdir -p "${version_dir}" \
    && cp "${system_php}" "${version_dir}" \
    && export CONFIGURE_OPTS="${PHP_CONFIGURE_OPTS}" \
    && export CFLAGS="${PHP_CFLAGS}" \
    && echo -e "${PREINSTALLED_VERSIONS}" | while read version;do \
        if [ ! -e "${PHPENV_ROOT}/versions/${version}" ];then \
            phpenv install $version;fi;done \
    && rm -rf "/tmp/php-build*"
