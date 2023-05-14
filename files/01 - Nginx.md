# Nginx

## Nginx VS Apache

- Apache is configured in what's called `Prefork mode` meaning that it set number of processes, each of which can serve single request at a time, regardless of whether that request is for a PHP script or an image. 

![alt text](./images/1.png)

- Nginx, on the other hand deals with requests asynchronously, meaning that a single nginx process serve multiple requests concrurrently just depending on the system resources available to the nginx process.

![alt text](./images/2.png)

- Nginx unlike Apache can't embed server side programming languages into it's own processes, meaning that all requests for dynamic content has to be dealt with by a completely separate process like PHP FPM and then reverse proxy back to the client via nginx.

![alt text](./images/3.png)

- Not having to deal with embedded programming languages like apache dose makes nginx a lot less resource hungry. This doesn't mean that the resources used for the processing of server side languages is simply freed up. Rather, they are being allocated elsewhere, like in the most common case of B to the FPM process.

- But it does mean that unlike Apache, the server side language modules don't need to be run for every single request the server receives.

![alt text](./images/4.png)

- Instead, Nginx will handle serving static resources without ever knowing about it, whereas Apache will handle every request with that costly overhead.

![alt text](./images/5.png)

- Nginx can't magically deliver data to the client any faster than the Internet connection will allow. But it can serve static resources much faster than Apache and handle a much larger number of concurrent requests.

- Remember, Nginx will serve static resources without the need to involve any server side languages, and this gives it quite an advantage over Apache.

- For handling concurrent requests, Nginx can potentially receive thousands of requests on a single processing thread and respond to them as fast as it can without turning down any of those requests.

- Apache, on the other hand, will accept requests up to the pre configured number and then simply reject the rest.

- How does Apache and Nginx handle incoming requests differently?
    * Nginx interprets incoming requests as URL locations whereas Apache prefers to interprets requests as filesystem loctions. 
