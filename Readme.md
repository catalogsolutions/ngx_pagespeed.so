# ngx_pagespeed.so
nginx dynamic module ngx_pagespeed.so

Built for nginx 1.10.3 that ships with Ubuntu 16.04LTS

## Usage

### git clone

```cmd
$ mkdir ~/tmp
$ cd ~/tmp
$ git clone https://github.com/catalogsolutions/ngx_pagespeed.so.git
$ cd tmp
```

### Copy to 

```cmd
$ sudo mkdir /usr/share/nginx/modules
$ cp ./ngx_pagespeed.so /usr/share/nginx/modules/
```

### Load Module

edit `/etc/nginx/nginx.conf`, e.g.

```conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;

load_module modules/ngx_pagespeed.so;

events {
        worker_connections 768;
        # multi_accept on;
}

http {
    ...
}
```

### Create Pagespeed Cache

```cmd
$ sudo mkdir /var/cache/ngx_pagespeed -p
$ sudo chown www-data:www-data -R /var/cache/ngx_pagespeed
```

### Configure Site

edit `/etc/nginx/sites-enabled/default`, e.g.

```conf
server {
    listen 80;
    
    pagespeed on;
    pagespeed FileCachePath /var/cache/ngx_pagespeed;

...
}

```