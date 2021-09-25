# Wordpress

```bash
sudo chown -R wpuser:www-data /var/www/wordpress

sudo find /var/www/wordpress -type d -exec chmod g+s {} \;

sudo chmod g+w /var/www/wordpress/wp-content

sudo chmod -R g+w /var/www/wordpress/wp-content/themes

sudo chmod -R g+w /var/www/wordpress/wp-content/plugins
```

## Wordress link
- https://vinta.ws/code/setup-scalable-wordpress-sites-on-kubernetes.html
- https://github.com/histeriks/Kubernetes-wordpress-php-fpm-nginx/
- https://github.com/kubernetes/ingress-nginx/issues/6602
- https://medium.com/@harsh.manvar111/kubernetes-wordpress-php-fpm-nginx-73cb4f9aef02

## Nginx
- https://www.digitalocean.com/community/tutorialshow-to-deploy-a-php-application-with-kubernetes-on-ubuntu-16-04-pt
- https://matthewpalmer.net/kubernetes-app-developer/articles/php-fpm-nginx-kubernetes.html