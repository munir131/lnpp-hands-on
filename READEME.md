### Add asdf in path
```
echo "export PATH=/opt/asdf-vm/bin/asdf:$PATH" >> ~/.zshrc
source .
```

### Install nginx
```
yay -S nginx
or
sudo pacman -S nginx 
```


### Check your nginx
```
cat /etc/nginx/nginx.conf 
```

###
```
sudo mkdir /etc/nginx/sites-available
sudo touch /etc/nginx/sites-available/default
```

```
server {
  # Example PHP Nginx FPM config file
  listen 80 default_server;
  listen [::]:80 default_server;
  root /usr/share/nginx/html;

  # Add index.php to setup Nginx, PHP & PHP-FPM config
  index index.php index.html index.htm index.nginx-debian.html;

  server_name localhost;

  location / {
    try_files $uri $uri/ =404;
  }

  # pass PHP scripts on Nginx to FastCGI (PHP-FPM) server
  location ~ \.php$ {
         try_files $uri =404;
         fastcgi_split_path_info ^(.+?\.php)(/.+)?$;
         # NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini

         # With php5-cgi alone:
         #fastcgi_pass 127.0.0.1:9000;
         # With php5-fpm:
         fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
         fastcgi_index index.php;
         include fastcgi_params;
 }

  # deny access to Apache .htaccess on Nginx with PHP, 
  # if Apache and Nginx document roots concur
  location ~ /\.ht {
    deny all;
  }
} # End of PHP FPM Nginx config example
```

### Install ps in container
```
apt-get update && apt-get install procps
```

### Start PHP-FPM
```
systemctl start php-fpm
```

### Install PHP

```
PHP_CONFIGURE_OPTIONS="--with-pgsql --with-openssl=/usr/include/openssl" asdf install php 8.2.5
```

### Create Table
```
CREATE TABLE users(id SERIAL primary key, name varchar(64));
INSERT INTO users (name) VALUES('munir'),('linus'),('james');
```

### Restart nginx
```
systemctl restart nginx.service
```