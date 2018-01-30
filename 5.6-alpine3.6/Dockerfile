FROM conchoid/docker-phpenv

ENV PREINSTALLED_VERSIONS "\
5.3.29\n\
5.4.45\n\
5.5.38\n\
5.6.32\n\
7.0.27\n\
7.1.13\n\
7.2.1"

RUN set -x \
    && echo -e "$PREINSTALLED_VERSIONS" | while read version;do \
        export CFLAGS="" \
        if [[ "$version" == "5.3."* ]];then \
            export CFLAGS="-lssl -lcrypto" \
        fi \
        phpenv install $version; done \
    && rm -rf "/tmp/php-build*"
