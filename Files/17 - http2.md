# [HTTP 2](../Code/15%2BHTTP2.conf)

- HTTP 2 is a binary protocol where HTTP 1 is a textual protocol.
- Binary data or ones and zeroes is a far more compact way of transferring data, and it greatly reduces the chance of errors during data transfer.
- HTTP 2 compress its response headers, which again reduces transfer time.
- HTTP 2 uses persistent connections. And those persistent connections are also multiplexed, meaning that multiple assets such as stylesheets, scripts and HTML can be combined into a single stream of binary data and transmitted over a single connection.
- But HTTP 1 requiring a dedicated connection for each resource.
- HTTP 2 can perform a server push, meaning that the client, the browser can be informed of assets such as scripts, images or stylesheets, along with the initial request for the page.
- Remember that opening a new connection is a time consuming process, which is why developers concatenate multiple JavaScript or access files into single file.
- Opening a connection requires a handshake between the client and the server, and for this to happen, headers need to be passed on both ends each time.

## How to enable and configure HTTP 2 on Nginx?
- Very importantly, a requirement of HTTP 2 is SSL or HTTPS meaning before we're able to use HTTP 2 will also have to configure the most basic SSL connection.

#

- step one is going to be adding the HTP to module to our install. (review [Add Dynamic Module](14%20-%20Adding%20Dynamic%20Modules.md))

- We're going to need is an SSL certificate for a production website. You'll of course want some legitimate certificates from a vendor or a service such as Let's Encrypt.
- We will generate a self signed certificate and private key perfectly fine for testing and development.

```
mkdir /etc/nginx/ssl
```
- Generate these test certificates using the open SSL command line tools
```
openssl req -x509 -days 10 -nodes -newkey rsa:2048 -keyout /etc/nginx/ssl/self.key -out /etc/nginx/ssl/self.crt  
```

- Enable HTTP 2 with SSL in nginx.conf
```
listen 443 ssl http2;
```
```
ssl_certificate /etc/nginx/ssl/self.crt;
```
```
ssl_certificate_key /etc/nginx/ssl/self.key;
```


## `Links`
- [How To Create a Self-Signed SSL Certificate for Nginx in Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-16-04)

