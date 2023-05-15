# [Logging](../Code/06%2BLogging.conf)

- Nginx provides us to log type's `error logs` and `access logs`.

- `error logs`, as the name suggests, for anything that failed or didn't happen as expected.
- `access logs` to log all requests to the server.


- Logging is an extremely important aspect of not only Nginx, but Web servers in general. As logs allow us to track down errors or even identify malicious users.

- logging is also enabled by default. So for that reason, most of the time, leaving the log configuration as is, will be fine.

- disabling logs for certain conditions or creating resource specific logs can both help lower resource usage and improve the log file structure.

- In our case, we set the path to the log files when we configured Nginx in the installation, which was `--http-log-path=/var/log/nginx/access.log` and `--error-log-path=/var/log/nginx/error.log`.
```
ls /var/log/nginx
```

- We can create custom log files or disable logging altogether for a given context by means of the `access_log` or `error_log`.

- Let's say we want to add access log for all requests to /secure not the default file;
```
location /secure {
      access_log /var/log/nginx/secure.access.log;
    }
```

- To see this new file:
```
ls /var/log/nginx
```

- It is possible to log this to both, however, by simply adding another access log with the global path, in which case we will get that log entry in both.

```
location /secure {
      access_log /var/log/nginx/secure.access.log;
      access_log /var/log/nginx/access.log;
    }
```

- Log directive's being one of the few directives you can use multiple times like this.

- Another common use of the LOG directive is to disable logging for certain requests, and in doing so reducing server load and keeping log files smaller.  particularly useful for sites receiving very high traffic

```
location /secure {
      access_log off;
    }
```

### `Links`
- [Configuring Logging](https://docs.nginx.com/nginx/admin-guide/monitoring/logging/)
- [Module ngx_http_log_module](http://nginx.org/en/docs/http/ngx_http_log_module.html)
- [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log)