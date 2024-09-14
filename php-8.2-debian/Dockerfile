FROM debian:bullseye

MAINTAINER Giuseppe Morelli <hello@giuseppemorelli.net>

RUN useradd -ms /bin/bash mainuser

RUN apt-get -y update \
    && apt-get -y install \
    apt-transport-https \
    ca-certificates \
    wget \
    curl

# RUN apt-get dist-upgrade -y

## install chrome headless
RUN apt-get install patch libnss3-tools pip -y
RUN pip install flare-floss

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | tee /etc/apt/trusted.gpg.d/google.asc >/dev/null
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor | tee /etc/apt/trusted.gpg.d/google.gpg >/dev/null

# RUN cd /tmp/ && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN cd /tmp/ && wget -O google-chrome.deb https://www.slimjet.com/chrome/download-chrome.php?file=files%2F102.0.5005.63%2Fgoogle-chrome-stable_current_amd64.deb
RUN apt-get install /tmp/google-chrome.deb -y

RUN wget -O "/etc/apt/trusted.gpg.d/php.gpg" "https://packages.sury.org/php/apt.gpg" \
    && sh -c 'echo "deb https://packages.sury.org/php/ bullseye main" > /etc/apt/sources.list.d/php.list'

RUN apt-get update \
    && apt-get -y install --no-install-recommends \
    apache2 \
    git \
    php8.2 \
    php8.2-common \
    php8.2-cli \
    php8.2-curl \
    php8.2-dev \
    php8.2-gd \
    php8.2-intl \
    php8.2-mysql \
    php8.2-mbstring \
    php8.2-xml \
    php8.2-xsl \
    php8.2-zip \
    php8.2-soap \
    php8.2-bcmath \
    php8.2-imagick	\
    php8.2-exif	\
    php8.2-opcache	\
    php8.2-bcmath \
    php8.2-ctype \
    php8.2-dom \
    php8.2-iconv \
    php8.2-sockets \
    php8.2-dev \
    php8.2-tokenizer \
    php8.2-phpdbg \
    php8.2-sqlite3 \
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

RUN apt-get update && \
    apt-get install -y ca-certificates curl gnupg && \
    mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

# TODO: add node version with parameter
RUN NODE_MAJOR=18 && \
    echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list

RUN apt-get update && \
    apt-get install nodejs -y

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install yarn -y

CMD ["/bin/bash"]
