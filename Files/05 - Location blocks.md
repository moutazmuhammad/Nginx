# Location blocks

- This is the most used context in any Ingenix configuration, and it's how will define and configure the behavior of specific URL.

```
server {
    location URL {

    }
}
```

- As we saw in the previous lesson, this standard behavior is great for static resources, such as our stylesheet to this image, etc. But if we request, for example, `ip/greet` or any other URL, Nginx cannot match a file and instead serves this default 404 page.

- So let's see how to use a custom location context and intercept that greet request and give it some hypothetical purpose.

- Back to the Nginx [configuration file](../Code/02%2BLocation%2BBlocks.conf) adding location context inside the server context.


## The Order Of Priority:
###   1 - Exact match [=]
###   2 - Preferential Prefix match [^~]
###   3 - REGEX match - case Insensitive [~*]
###   4 - Prefix match [ ]