# ADD HEADER INSTALL ON CENTOS 7

## INSTALL BASIC PACKAGE
````
yum install gcc -y
yum install pcre-devel -y
yum install zlib-devel -y
yum install gd gd-devel -y
````

## EXTRACT

````
tar -xzvf nginx-1.20.1.tar.gz
cd nginx-1.20.1/
````

## CONFIGURE

````
./configure --prefix=/var/www/html --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf \
--http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --with-pcre  \
--lock-path=/var/lock/nginx.lock --pid-path=/var/run/nginx.pid --with-http_ssl_module \
--with-http_image_filter_module=dynamic --modules-path=/etc/nginx/modules --with-http_v2_module \
--with-stream=dynamic --with-http_addition_module --with-http_mp4_module \
--add-module=/root/nginx-addon/headers-more-nginx-module
````

## MAKE INSTALL

````
make
make install
````

## COMMAND CONTROL

````
nginx
nginx -s stop
nginx -s reload
````

## ADD IN CONFIG

````
server_tokens off;
more_set_headers "Server: ";
````

### ORIGINAL PACKAGE

````
git clone https://github.com/openresty/headers-more-nginx-module.git
wget 'http://nginx.org/download/nginx-1.20.1.tar.gz'
````
