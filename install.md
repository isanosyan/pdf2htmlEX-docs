How to install
==============

I found that author of pdf2htmlEX maintains his own ppa repository, so installing in ubuntu is pretty much simple:

```
$ sudo -i
# add-apt-repository ppa:coolwanglu/pdf2htmlex
# apt-get update
# apt-get install -y poppler-data
# apt-get install -y pdf2htmlex
```

That's it. Now you should be able to run pdf2htmlEX and check the version:

```
# pdf2htmlEX -v
pdf2htmlEX version 0.9
Copyright 2012,2013 Lu Wang <coolwanglu@gmail.com>
Libraries: poppler 0.20.3, libfontforge 20120731
Default data-dir: /usr/share/pdf2htmlEX
```

Installing the webapp
=====================

The management console (web application) is built with [Silex](http://silex.sensiolabs.org/) microframework.

### Install the web server environment

```
$ sudo -i
# apt-get install -y nginx php5-fpm php5-cli
# mkdir /var/www/pdf2htmlEX
# chown www-data:www-data /var/www/pdf2htmlEX
```

### Configure the environment

Create file `/etc/nginx/sites-enabled/webroot` with the following contents:

```
upstream phpfcgi {
    server 127.0.0.1:9000;
}
server {
    listen 80;

    root /var/www/pdf2htmlEX/web;

    error_log /var/log/nginx/pdf2htmlEX.error.log;
    access_log /var/log/nginx/pdf2htmlEX.access.log;

    client_max_body_size 100m;

    #site root is redirected to the app boot script
    location = / {
        try_files @site @site;
    }

    #all other locations try other files first and go to our front controller if none of them exists
    location / {
        try_files $uri $uri/ @site;
    }

    #return 404 for all php files as we do have a front controller
    location ~ \.php$ {
        return 404;
    }

    location @site {
        fastcgi_pass   phpfcgi;
        include fastcgi_params;
        fastcgi_param  SCRIPT_FILENAME $document_root/index.php;

        fastcgi_buffers      16 16k;
        fastcgi_buffer_size  32k;
    }
}
```

### Install the project

Run following commands:

```
# service nginx restart
# su www-data -c bash
$ cd /var/www/pdf2htmlEX
$ git clone https://github.com/isanosyan/pdf2htmlEX-web.git .
$ curl -sS https://getcomposer.org/installer | php
$ chmod +x composer.phar
$ ./composer.phar install
```

Done.