# Creating a basic virtual host

### creating a basic virtual host to serve static files from a directory on our server.
- To demonstrate this, I've created a directory called Sites [demo-site](../demo-site.zip) at the root of my server 
- Inside demo-site: I've uploaded a very simple single page website.
- The files I've uploaded consists of a single HTML file indexed on HTML access file, which is linked to in indexed HTML and a PMG image.

- The main configuration file we're going to edit is `etc/nginx/nginx.conf`, which at the moment is still serving that default holding page.