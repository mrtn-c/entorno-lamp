FROM delboy1978uk/php81:1.1.0
COPY ./php/php-ini-overrides.ini /usr/local/etc/php/conf.d/99-overrides.ini
COPY ./php/ssmtp.conf /etc/ssmtp/ssmtp.conf
# Instala Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --filename=composer
RUN rm composer-setup.php
RUN chmod +x composer
RUN mv composer /usr/local/bin/composer

RUN useradd --uid 1000 --create-home php
RUN echo "export PATH=$PATH:bin:vendor/bin" > /home/php/.bashrc
COPY ./certificates/proxyman_ca.crt /usr/local/share/ca-certificates/proxyman_ca.crt
RUN chmod 644 /usr/local/share/ca-certificates/proxyman_ca.crt && update-ca-certificates

USER root

# Cambia los permisos para que tanto www-data como php puedan acceder a los archivos y directorios
RUN chown -R www-data:php /var/www/html

# Establece permisos en los archivos y directorios
RUN find /var/www/html -type d -exec chmod 755 {} \;
RUN find /var/www/html -type f -exec chmod 644 {} \;

# Cambia al usuario www-data
USER www-data

# Establece el directorio de trabajo de PHP
WORKDIR /var/www/html
RUN ls

# Ejecuta composer install para instalar las dependencias de PHP
