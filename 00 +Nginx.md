# NGINX vs APACHE

- In Apache: 
    + each process can serve a single request.
    + can embed server side programming languages.

- In Nginx:
    + deals with requests asynchronously.
    + each process can serve multiple requests.
    + can't embed server side programming languages into it's own process meaning that all requests for
        dynamic contant has to be dealt with by a separte process (like PHP-FPM) and the reverse proxy back to the client via nginx.
    + can serve static contant faster than apache and handle a much concurrent requests.

- Install Nginx through package manager:
    ```sh
     apt update 
    ```
    ```sh
    apt install nginx

- Install Nginx from Source Code:
    ```sh 
    apt update
    ```
    ```sh 
    wget (+link from nginx.org)
    ```
    ```sh 
    ls            => nginx-1.12.10.tar.gz
    ```
    ```sh 
    tar -zxvf nginx-1.12.10.tar.gz
    ```
    ```sh 
    cd nginx-1.12.10/
    ```
    * This for install compilar and development tools:
    ```sh 
    apt install build-essential
    ```
    * This to install dependences for nginx:
    ```sh 
    apt install libpcre3 libpcre3-dev zlib1g  zlib1g-dev libssl-dev
    ```
    * Configure nginx with flags:
    ```sh 
    ./configre --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid  --modules-path=/etc/nginx/modules
    ```
    > Note: you can add flags for dynamic modules in last command

    > To find all flags and modules use command  ./configre --help
    ```sh
    make
    ```
    ```sh
    make install
    ```

- You need to add Nginx service (systemd service)
    ```sh
    vim /lib/systemd/system/nginx.service
    ```
    
    ```sh
    [Unit]
    Description=The NGINX HTTP and reverse proxy server
    After=syslog.target network-online.target remote-fs.target nss-lookup.target
    Wants=network-online.target

    [Service]
    Type=forking
    PIDFile=/var/run/nginx.pid
    ExecStartPre=/usr/bin/nginx -t
    ExecStart=/usr/bin/nginx
    ExecReload=/usr/bin/nginx -s reload
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target
    ```

    ```sh
    systemctl start nginx
    ```
    ```sh
    systemctl enable nginx
    ```
    ```sh
    systemctl status nginx
    ```
