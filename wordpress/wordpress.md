# Wordpress

## Links

### Wordress

- <https://vinta.ws/code/setup-scalable-wordpress-sites-on-kubernetes.html>
- <https://github.com/histeriks/Kubernetes-wordpress-php-fpm-nginx>
- <https://github.com/kubernetes/ingress-nginx/issues/6602>
- <https://medium.com/@harsh.manvar111/kubernetes-wordpress-php-fpm-nginx-73cb4f9aef02>

### Nginx

- <https://www.digitalocean.com/community/tutorials/how-to-deploy-a-php-application-with-kubernetes-on-ubuntu-16-04-pt>
- <https://matthewpalmer.net/kubernetes-app-developer/articles/php-fpm-nginx-kubernetes.html>

## How to generate a custom image

- <https://github.com/docker-library/wordpress/tree/master/latest/php8.0/fpm-alpine>

### Setup pre build

- Change the chmod level on Dockerfile

```diff
mkdir wp-content; \
    for dir in /usr/src/wordpress/wp-content/*/ cache; do \
        dir="$(basename "${dir%/}")"; \
        mkdir "wp-content/$dir"; \
        done; \
    chown -R www-data:www-data wp-content; \
-   chmod -R 777 wp-content
+   chmod -R 755 wp-content
```

- Append `pdo_mysql` extension on docker-php dependencies

```diff
    docker-php-ext-install -j "$(nproc)" \
        bcmath \
        exif \
        gd \
        mysqli \
        zip \
+       pdo_mysql \
```

- Provide execute permission to `docker-entrypoint` file.

```properties
chmod +x docker-entrypoint.sh
```

- Create config folders

php.ini

```properties
mkdir -p data/php/conf.d
touch data/php/conf.d/php.ini
```

```ini
file_uploads=On
memory_limit=64M
upload_max_size=64M
max_execution_time=600
expose_php=Off
```

nginx.conf

```properties
mkdir -p data/nginx/my_includes_files
touch data/nginx/nginx.conf
```

```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    
    access_log off;
    #access_log /var/log/nginx/access.log
    error_log /var/log/nginx/error.log;

    root /var/www/html;
    server_name  _;
    index index.php;

    server_tokens off;
    #include /etc/nginx/my_includes_files/*.conf

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param   PATH_INFO       $fastcgi_path_info;
        fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```
