FROM php:8.3-cli

WORKDIR /app

# Set an argument for the Node.js major version (default is 20)
ARG NODE_MAJOR_VERSION=20

# Update packages, install dependencies, and set up Node.js repository
RUN apt-get update && apt-get upgrade -y && \
\
    # install dependencies and nodejs
    curl -fsSL https://deb.nodesource.com/setup_$NODE_MAJOR_VERSION.x | bash - && \
    apt-get install -y nodejs zip unzip libicu-dev && \
\
    # Install Composer
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && \
\
    # Remove unnecessary files and cleanup to reduce the Docker image size
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
