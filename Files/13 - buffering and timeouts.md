# [Optimizing Processes By Configuring `Buffer Sizes` And `Timeouts`](../Code/10%2BBuffers%2B%26%2BTimeouts.conf)


-  Note that whilst configuring processes is a fairly easy and measurable task, buffer sizes and time outs is the complete opposite. This being as they're not so much dependent on the server, but more the nature of the requests to the server.

- In fact, I'd suggest leaving these as their default values if you're unsure about why you're tweaking them at all.

## What a buffer is?
- Buffering is when a process or an engine work in this case reads data into memory or RAM before writing it to its next destination.
- For example, Nginx receives a request which it reads from a TCP port port and in this case writes that request data to memory, which is buffering, or if the buffer is too small for the amount of data being read, write some of it to disk.
- Layer of protection between reading and writing of data.

## What a Timeouts is?
- Simply suggest a cutoff time for a given event.
- For example, if receiving a request from a client, stop after a certain number of seconds, thus preventing a client from sending an endless stream of data and eventually breaking the server.

# 


## Buffer size for POST submissions

```
client_body_buffer_size 10K;
```
- This directive then setting the amount of memory to allocate for buffering.
- Increasing this number to more than what we need will allocate and essentially waste memory on our server.
- Making it too small will require Nginx to write part of this buffer to disk, which is a lot slower than writing it to memory.

```
client_max_body_size 8m;  
```
- Don't accept post requests of more than 8 megabytes if it is larger than eight megabytes, the server will respond with a 413 error, which is request entity to large.


## Buffer size for Headers
```
client_header_buffer_size 1k;
````
- The amount of memory to allocate to reading request headers.


## Max time to receive client headers/body
```
client_body_timeout 12;
```
```
client_header_timeout 12;
``` 
- You need to put these two with the same value


  
## Max time to keep a connection open for
```
keepalive_timeout 15;
```
- This directive sets the amount of time Nginx should keep a connection to a client open for in case more data is on the way.
- This is extremely useful when, a client is requesting a number of files and keeping a connection open reduces the time it takes to open another new connection, equally not wanting to leave connections open for too long as this can result in our pool of max connections.

## Max time for the client accept/receive a response
```
send_timeout 10;
```

## Skip buffering for static files
```
sendfile on;
```

## Optimise sendfile packets
```
tcp_nopush on;
```


## `Links`
- [Configuration file measurement units](http://nginx.org/en/docs/syntax.html)
