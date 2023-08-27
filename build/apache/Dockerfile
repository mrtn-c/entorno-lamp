FROM httpd:2.4

# Copiar los archivos de configuración personalizados
COPY httpd/httpd-vhosts.conf /usr/local/apache2/conf/httpd.conf
COPY httpd/httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf



# Copiar los certificados al contenedor
COPY /certificates/mydomain.crt /etc/ssl/certs/mydomain.crt
COPY /certificates/mydomain.key /etc/ssl/certs/mydomain.key



# Configurar Apache para SSL
RUN sed -i '/<VirtualHost \*:80>/a \
    <VirtualHost \*:443>\n\
        ServerName awesome.scot\n\
        DocumentRoot /var/www/html/public\n\
        SSLEngine on\n\
        SSLCertificateFile /etc/ssl/certs/mydomain.crt\n\
        SSLCertificateKeyFile /etc/ssl/certs/mydomain.key\n\
        <Directory "/var/www/html">\n\
            DirectoryIndex index.php\n\
            FallbackResource /index.php\n\
            Options -Indexes +FollowSymLinks\n\
            AllowOverride FileInfo All\n\
            Require all granted\n\
        </Directory>\n\
        ProxyPassMatch ^/(.*\.php)$ fcgi://php:9000/var/www/html/\n\
    </VirtualHost>' /usr/local/apache2/conf/extra/httpd-vhosts.conf

