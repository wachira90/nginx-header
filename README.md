# ADD HEADER INSTALL ON CENTOS 7

## INSTALL BASIC PACKAGE
````
yum install gcc pcre-devel zlib-devel gd gd-devel openssl-devel -y
````

## DIRECTORY

````
/root/nginx-header/
/root/nginx-1.20.1.tar.gz

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
--add-module=/root/nginx-header
````

## MAKE INSTALL

````
make
make install
````

## ADD IN CONFIG

````
server_tokens off;
more_set_headers "Server: ";
````
## ADD SERVICE

nano /lib/systemd/system/nginx.service

````
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/sbin/nginx -t
ExecStart=/sbin/nginx
ExecReload=/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
````

## COMMAND CONTROL

````
nginx
nginx -s stop
nginx -s reload

systemctl start nginx.service
systemctl stop nginx.service
systemctl restart nginx.service
systemctl status nginx.service

systemctl enable nginx
systemctl disable nginx
````

### ORIGINAL PACKAGE

````
git clone https://github.com/openresty/headers-more-nginx-module.git
wget 'http://nginx.org/download/nginx-1.20.1.tar.gz'
````
