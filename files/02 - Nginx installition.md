# [Installation](https://www.alibabacloud.com/blog/how-to-build-nginx-from-source-on-ubuntu-20-04-lts_597793) (Ubuntu)

## Installing our custom build of Nginx


> Note: \
>  [nginx.org](http://nginx.org/en/docs) is where we'll look for the majority of our documentation. \
>  [nginx.org](https://nginx.com) is the flashier product side of Nginx.

Update the Ubuntu's package manager

```
sudo apt-get update 
```

- The next step is downloading the latest engine exhaust code.
- [Here](http://nginx.org/en/download.html) we have source code links to the mainline version, which is what will be using the stable version.

-  Download the source code

```
wget http://nginx.org/download/nginx-1.23.4.tar.gz
```

- Extract the file 

```
tar -zxvf nginx-1.23.4.tar.gz
```

- Change directory into it 
```
cd nginx-1.23.4
```

- Now, install development libraries along with source code compilers.
```
sudo apt-get install build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev
```

- Now we have to use the configure flag for configuring NGINX by using this command.
```
./configure \
 --prefix=/var/www/html \
 --sbin-path=/usr/sbin/nginx \
 --conf-path=/etc/nginx/nginx.conf \
 --http-log-path=/var/log/nginx/access.log \
 --error-log-path=/var/log/nginx/error.log \
 --with-pcre  \
 --lock-path=/var/lock/nginx.lock \
 --pid-path=/var/run/nginx.pid \
 --with-http_ssl_module \
 --with-http_image_filter_module=dynamic \
 --modules-path=/etc/nginx/modules \
 --with-http_v2_module \
 --with-stream=dynamic \
 --with-http_addition_module \
 --with-http_mp4_module
```
> The main benefit of building Ingenix from source is the ability to add custom modules or essentially extend the standard Ingenix functionality, something you cannot do using a package manager.

> Note 1: that Nginx modules exist in two forms: bundled modules and third party modules, \
> third party modules being modules that's developed and maintained by third party developers and needs to be downloaded and compiled with Nginx to use. \
> Bundled modules, on the other hand, being modules that come with the engine exhaust. Like, for example, the HTTP SSL module.

>  To see a comprehensive list of [modules](http://nginx.org/en/docs/) available with the engine exhaust.


- There many modules comes with NGINX pre-installed If you don't need a module that is built by default, you can disable it by naming it with the `--without-< MODULE-NAME >` option on the configure script, for example:
```
./configure --without-http_empty_gif_module
```


- After custom configuration complete we can now compile NGINX source code by using this command :
```
make
```

- This will take quite a bit of time and once that's done install the compiled source code by using this command.
```
make install
```

- Start NGINX by using this command
```
nginx
```

- Now we have successfully installed NGINX. To verify this, check the NGINX version by using this command.
```
nginx -V
```

# Adding a NGINX Service

- We can confirm that NGINX is running by checking for the process.
```
ps aux | grep nginx 
```

- So with NGINX running in the background, let's see how to send it a stop signal. Using the standard command-line tools.
```
nginx -s stop
```

### So next, let's add that `systemd` service.

- Create an Nginx systemd unit file by using nano editor
```
nano /lib/systemd/system/nginx.service
```

- and paste this script
```
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target
        
[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true
        
[Install]
WantedBy=multi-user.target
```
- Start your NGINX by using systemd with this command.
```
systemctl restart nginx
```

- You can also check the status of NGINX whether it is running or not by using this command.
```
systemctl status nginx
```

- So to enable start-up on boot, run this command.
```
systemctl enable nginx
```