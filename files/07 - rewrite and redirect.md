# [Rewrite and Redirect](../04%2BRewrites%2B%26%2BRedirects.conf)

- The two directives we can use for rewriting requests is the `rewrite directive` and the `return directive`.
```
rewrite + pattern URL;
```

```
return + status + URL;

return 200 "Hello World";
```

- The return statement, as we've been using it, takes a status code and response data or strings.
- But in the case of that response code being a 300 variant, which is for redirects the return directives behavior changes in the reden except a URI as the second parameter.
```
return 307 /some/path;  
```

- For example, at the moment we can access the demo site's image by requesting `thumb.png` , But let's say we also want to serve this image for `/logo`, which obviously right now returns a 404.

```
location /logo {
    return 307 /thumb.png;
}
```
> But very importantly, note that the euro changed to thumb.png, which is essentially the main difference between rewrites and redirects.

- A `redirect` simply tells the client performing the request where to go instead.
- A `rewrite`, on the other hand, mutates the URAI internally. So let's see an example:
    - we can say rewrite pass a regular expression with which to match the URI

```
rewrite ^/user/\w+ /greet;
```

```
location /greet {
    return 200 "Hello User"
}
```

- \w+ meaning more than one word.
- Now is the important thing to understand about rewrites. When a URI is rewritten, it also gets re-evaluated by Nginx as a completely new request, meaning at this point here the rewritten great URI starts right from the top again and will get reevaluated again. The re-evaluation makes rewrites very powerful, but also requires more system resources than return.


- Another important and powerful feature of rewrites is the ability to capture certain parts of the original URI using standard regular expression capture groups. For example, let's say we want to capture the user name `/user/username` .
```
rewrite ^/user/(\w+)/(another thing) /greet/$1 $2;
```

```
location = /user/moutaz {
    return 200 "Hello Moutaz";
}
```

## Two times rewriting
```
rewrite ^/user/(\w+) /greet/$1;
```

```
rewrite /greet/moutaz /thumb.png;
```


## Don't allow a URI to be rewritten anymore using `last`

```
rewrite ^/user/(\w+) /greet/$1 last;
```

