# [Variables](../Code/03%2BVariables.conf)

### variables exist in two forms:
- variables we set ourselves.
```
set $var 'something';
```
- Nginx own built in variables.
```
$http , $uri, $args
```

- We can find a list of these Nginx variables in the [nginx.org documentation](http://nginx.org/en/docs/varindex.html) alphabetical index of variables, which lists each of the available variables with the module that makes it available.

- Modules like `ngx_http_core_module` and `ngx_http_log_module` already being part of Nginx, so you don't have to manually add them.



# Condition
> Note that the use of Nginx conditionals inside location contexts is highly discouraged, as this can lead to some very unexpected behavior.



### `Links`
- [If is Evil](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/)

- [variables](http://nginx.org/en/docs/varindex.html)