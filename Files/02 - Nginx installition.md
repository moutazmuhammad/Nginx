# [Installation](https://www.alibabacloud.com/blog/how-to-build-nginx-from-source-on-ubuntu-20-04-lts_597793) (Ubuntu)

## Installing our custom build of Nginx


> Note: \
>  [nginx.org](http://nginx.org/en/docs) is where we'll look for the majority of our documentation. \
>  [nginx.org](https://nginx.com) is the flashier product side of Nginx.

- make sure that we have no permission issue on the installation & configuration.
```
sudo su
```

- Update the Ubuntu's package manager

```
apt update 
```

### Install Dependencies

- Run this command to install Nginx dependencies
```
apt update -y && apt-get install git build-essential libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev libgd-dev libxml2 libxml2-dev uuid-dev
```

### Download Nginx Source Code
- Before you download the Nginx source code, you can visit [nginx.org](http://nginx.org/en/download.html) to see the Nginx version available now. After that you can download them by running this command:
```
wget http://nginx.org/download/nginx-<version>.tar.gz1
```

- Extract the downloaded file
```
tar -zxvf nginx-<version>.tar.gz1
```

### Build & Install Nginx
- After extract the file, go to the nginx directory
```
cd nginx-<version>
```

- Now is the time to configure Nginx that suits your need, this is where you put in the module you want to include in Nginx using the `./configure` command. The full documentation is in here: [Building Nginx from Sources](http://nginx.org/en/docs/configure.html). For now, I will give you the minimum configure option so you can build a good load balancer, reverse proxy, or webserver. Run this command to configure Nginx:

```
./configure \
    --prefix=/etc/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --pid-path=/run/nginx.pid \
    --sbin-path=/usr/sbin/nginx \
    --with-http_ssl_module \
    --with-http_v2_module \
    --with-http_stub_status_module \
    --with-http_realip_module \
    --with-file-aio \
    --with-threads \
    --with-stream \
    --with-stream_ssl_preread_module
```

- After that, run this command to build & install the Nginx
```
make
```

```
make install
```

- To verify the installation, you can check the Nginx version
```
nginx -V
```

- Also notice that the Nginx folder will be created at `/etc/nginx` that provide the default `nginx.conf` and other file.

## Create Systemd File
- To make Nginx easier to manage, we can build a systemd file. First, create a new file in the systemd folder:
```
vim /lib/systemd/system/nginx.service
```

- And then copy & paste this config to the file
```
[Unit]
Description=Nginx Custom From Source
After=syslog.target network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

- Now you can control Nginx using systemd, just like this:
```
systemctl start nginx
```

- Enable Nginx service so it will auto start when the server boot
```
systemctl enable nginx
``````

- Other commands
```
service nginx stop
```

```
service nginx reload
```