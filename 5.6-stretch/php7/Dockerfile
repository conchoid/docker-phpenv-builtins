FROM conchoid/docker-phpenv:v1-12-5.6-stretch

ENV PHP_CONFIGURE_OPTS "--disable-fpm --disable-cgi"
ENV PHP_AUTOCONF /usr/bin/autoconf2.59
ENV PREINSTALLED_VERSIONS "\
7.0.33\n\
7.1.25\n\
7.2.13\n\
7.3.0"

RUN phpenv global system \
    && system_php_ver=$(php -v | head -1 | sed -e "s/^PHP \([0-9.]*\).*$/\1/") \
    && version_bin_dir="${PHPENV_ROOT}/versions/${system_php_ver}/bin" \
    && mkdir -p "${version_bin_dir}" \
    && cp "$(phpenv which php)" "${version_bin_dir}" \
    && cp "$(phpenv which php-config)" "${version_bin_dir}" \
    && cp "$(phpenv which phar)" "${version_bin_dir}" \
    && cp "$(phpenv which phar.phar)" "${version_bin_dir}" \
    && export CONFIGURE_OPTS="${PHP_CONFIGURE_OPTS}" \
    && export CFLAGS="${PHP_CFLAGS}" \
    && echo "${PREINSTALLED_VERSIONS}" | while read version;do \
        if [ ! -e "${PHPENV_ROOT}/versions/${version}" ];then \
            phpenv install $version \
            && phpenv global $version \
            # Add the timezone settings to php.ini to avoid date function wargnings.
            && php --ini | grep 'Loaded Configuration File' | awk -F':' '{ print $2 }' | xargs -i /bin/sh -c 'echo "[Date]\ndate.timezone = UTC" >> {}' \
            # validate php.ini
            && [ $(php --ini 2>&1 >/dev/null | wc -l) = "0" ] || exit 1 \ 
        ;fi \
    ; done \
    && rm -rf "/tmp/php-build*" \
    && phpenv global system

