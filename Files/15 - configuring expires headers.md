# [configuring expires headers](../Code/12%2BHeaders%2B%26%2BExpires.conf)

- They're essentially a response header informing the client or browser how long it can cache that response for.

-  For example, let's say we have an image or more specifically a photo on our website that photo data isn't realistically going to change all that often, meaning we can tell the browser to cache a copy of the photo for a relatively long time, and in doing so, avoid any future requests for that photo, drastically improving website load times and often overlooked a reduction in requests to our server.