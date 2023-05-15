# [try_files](../Code/05%2BTry%2BFiles%2B%26%2BNamed%2BLocations.conf)

- As with the return and rewrite directives can be used in the server context. So applying to all incoming requests.
```
server{

    try_files path1 path2 final;
}
```
- OR inside a location context
```
server{

    location / {
        try_files path1 path2 final;
    }
}
```

- what `try_files` allows us to do is have Nginx check for a resource to respond with in any number of locations relative to the root directory, with a final argument that results in a rewrite and re-evaluation, as with the rewrite directive.

- This is a directive which being so unique in its behavior, I suggest you really try out in a number of ways using a simple test configuration, but nonetheless will cover some arbitrary examples.

```
server{

    try_files /thumb.png /greet;
}
```
- So what this directive is doing then all the time being in the server context is checking whether `/sites/demo/thumb.png` exists. And if it does serve it, if, however this first argument doesn't exist, move on and try the next one and so on.
- In our case, thumb.png definitely exists relative to the root directory, so there should be served for all requests.

> Note:  the requests, checks, if this first argument exists and serves it regardless of the request you. \n
> However, when try_files reaches its last argument, that argument is treated as an internal rewrite.meaning in this case, and only in this case will the rewritten request also be re-evaluated.

-  The try_files directive is used with Ingenix variables, for example: first check the request as it is, we can add as the first argument here, the variable URI, meaning before anything else, try the URI.
```
try_files $uri /thumb.png /greet;
```

- Get friendly message using `named location [@]` means assigning a name to a location context and using a directive such as try_files use that location by its name, ensuring no re-evaluation has to happen on that final argument, but instead just a definite call to the name location to name a location.

```
server {
    try_files $uri /cat.png /greet @friendly_404;

    location @friendly_404 {
      return 404 "Sorry, that file could not be found.";
    }
}
```
