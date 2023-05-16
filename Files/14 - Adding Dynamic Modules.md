# [Adding Dynamic Modules](../Code/11%2BAdding%2BDynamic%2BModules.conf)

- Dynamic modules being modules we can load selectively from the Nginx configuration, unlike static modules, which is always loaded.

- Note that adding standard modules is exactly the same as adding dynamic modules as is upgrading Nginx itself to a newer version.

- To add new modules to Nginx will have to rebuild Nginx from source

## 1- Downloading NGINX and module source code
- You'll need to compile this against the same version of NGINX that's currently installed. You can find that by running 
```
nginx -v
```

```
wget https://nginx.org/download/nginx-1.14.0.tar.gz
```

```
tar zxf nginx-1.14.0.tar.gz
```

```
cd nginx-1.14.0
```

## 2- To see a list of dynamic modules available with the source code download.
```
./configure --help | grep dynamic
```

## 3- Find the NGINX compile flags
- To make our module compatible with the existing NGINX binary, we need to use the same compile flags. We can find those by running the following command:
```
nginx -V
```

## 4- Compiling the module
```
./configure --prefix=/etc/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/run/nginx.pid --sbin-path=/usr/sbin/nginx --with-http_ssl_module --with-http_v2_module --with-http_stub_status_module --with-http_realip_module --with-file-aio --with-threads --with-stream --with-stream_ssl_preread_module 

ADD THE NEW FLAG FOR YOUR DYNAMIC MODULE + --modules=/etc/nginx/modules
```


```
make
```

```
make install
```

```
systemctl reload nginx
```


## Now You can use the new module inside nginx.conf file.


## `Links`
- [How to Compile Dynamic NGINX Modules](https://gorails.com/blog/how-to-compile-dynamic-nginx-modules)