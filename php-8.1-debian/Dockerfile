FROM debian:bullseye

MAINTAINER Giuseppe Morelli <hello@giuseppemorelli.net>

RUN useradd -ms /bin/bash mainuser

RUN apt-get -y update \
    && apt-get -y install \
    apt-transport-https \
    ca-certificates \
    wget

RUN apt-get dist-upgrade -y

## install chrome headless
RUN apt-get install patch libnss3-tools pip -y
RUN pip install flare-floss
# RUN cd /tmp/ && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN cd /tmp/ && wget -O google-chrome.deb https://www.slimjet.com/chrome/download-chrome.php?file=files%2F102.0.5005.63%2Fgoogle-chrome-stable_current_amd64.deb
RUN apt-get install /tmp/google-chrome.deb -y

RUN wget -O "/etc/apt/trusted.gpg.d/php.gpg" "https://packages.sury.org/php/apt.gpg" \
    && sh -c 'echo "deb https://packages.sury.org/php/ bullseye main" > /etc/apt/sources.list.d/php.list'

RUN apt-get update \
    && apt-get -y install --no-install-recommends \
    apache2 \
    git \
    php8.1 \
    php8.1-common \
    php8.1-cli \
    php8.1-curl \
    php8.1-gd \
    php8.1-intl \
    php8.1-mysql \
    php8.1-mbstring \
    php8.1-xml \
    php8.1-xsl \
    php8.1-zip \
    php8.1-soap \
    php8.1-bcmath \
    php8.1-imagick	\
    php8.1-exif	\
    php8.1-opcache	\
    php8.1-bcmath \
    php8.1-ctype \
    php8.1-dom \
    php8.1-iconv \
    php8.1-sockets \
    rsync \
    unzip \
    rsync \
    curl \
    && apt-get clean \
    && rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/* \
    /usr/share/man \
    /usr/share/doc \
    /usr/share/doc-base

RUN curl -LO https://getcomposer.org/composer.phar \
    && chmod +x ./composer.phar \
    && mv ./composer.phar /usr/local/bin/composer

RUN wget https://get.symfony.com/cli/installer -O - | bash && \
mv /root/.symfony5/bin/symfony /usr/local/bin/symfony && \
chmod 777 /usr/local/bin/symfony

CMD ["/bin/bash"]