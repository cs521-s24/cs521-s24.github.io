---
layout: assignment
due: 2024-04-30 23:59:59 -0800
permalink: assignments/lab07.html
title: lab07 - HTTP server part 2
github_url: https://classroom.github.com/a/lCkQzIpR
published: true
---

## Requirements

In this assignment you will extend the PING/PONG server to implement
1. asynchronous network I/O using [`poll()`](https://linux.die.net/man/2/poll)
2. Basic [HTTP](https://datatracker.ietf.org/doc/html/rfc2616) requests

## Implementation Notes

### How to use poll()
1. The `poll()` takes an array of `struct pollfd` elements 
```sh
           struct pollfd {
               int   fd;         /* file descriptor */
               short events;     /* requested events */
               short revents;    /* returned events */
           };
```
1. Each `struct pollfd` wraps an `int` file descriptor, and includes some [flags](https://sites.uclouvain.be/SystInfo/usr/include/bits/poll.h.html).
1. We want to know when there is data to read on the file descriptor, so we set the `pollfd`'s `events` field to `POLLIN`.
1. When `poll()` returns, it tells us how many of the `struct pollfd` elements have input we can read.
1. We loop over all of the `pollfd`s in the array, looking for `(revents & POLLIN) != 0`
1. The file descriptor in that `pollfd` can be read with `recv()`. The `flags` is set to be 0 when no options are necessary.


### How to parse HTTP GET requests
1. Since HTTP requests are terminated by a `'\n'` you should `recv()` from a readable file descriptor into a buffer until you encounter a `'\n'`
1. The HTTP `Request-Line` contains a "method", a Uniform Resource Identifier (URI) and the protocol version, e.g. `GET / HTTP/1.1`. You should parse the request line into those pieces. 
1. If the request line contains a `GET` for `/` you should write a successful response into the file descriptor. Here is an example successful response:
    ```
    HTTP/1.1 200 OK
    Content-Type: text/html
    Content-Length: <length in bytes>

    <!DOCTYPE html>
    <html>
        <body>
          Hello CS 521
      </body>
    </html>
    ```
1. If the request contains a method other than `GET` or a URI other then `/` you should write a error response into the file descriptor. Here is an example error response for requesting a file that doesn't exist on the server (404 Not Found).
    ```
    HTTP/1.1 404 Not Found
    Content-Type: text/html
    Content-Length: <length in bytes>

    <!DOCTYPE html>
    <html>
        <body>
          Not found
      </body>
    </html>
    ```
1. 200 and 404 are HTTP response status codes. Here is [the full list](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). 

## Example Output

The autograder test cases for lab07 use `wget` as an http client, rather than `telnet` or `ncat`

```sh
$ ./lab07 -p 9001 &
[1] 14205
$ wget localhost:9001/ -O index.html
--2023-04-27 20:45:29--  http://localhost:9001/
Resolving localhost (localhost)... ::1, 127.0.0.1
Connecting to localhost (localhost)|::1|:9001... failed: Connection refused.
Connecting to localhost (localhost)|127.0.0.1|:9001... connected.
HTTP request sent, awaiting response... 200 OK
Length: 59 [text/plain]
Saving to: ‘index.html’

index.html          100%[===================>]      59  --.-KB/s    in 0s

2023-04-27 20:45:29 (13.9 MB/s) - ‘index.html’ saved [59/59]

$ cat index.html
<!DOCTYPE html>
<html>
<body>
Hello CS 521
</body>
</html>

Connection closed by foreign host.

$ wget localhost:9001/wrong -O wrong.html
--2023-04-27 20:46:56--  http://localhost:9001/wrong
Resolving localhost (localhost)... ::1, 127.0.0.1
Connecting to localhost (localhost)|::1|:9001... failed: Connection refused.
Connecting to localhost (localhost)|127.0.0.1|:9001... connected.
HTTP request sent, awaiting response... 404 Not Found
2023-04-27 20:46:56 ERROR 404: Not Found.


```

## Rubric

1. We will use autograder to test lab07 as follows:
    1. 49 pts for returning the default index page given above
    1. 49 pts for returning the not-found page given above
    1. 1 pt each for successfully starting and stopping the server
1. Remember to include `port.txt` like we did for lab07
1. Please don't commit the `*.tmp` or `*.html` files that autograder creates. 
You may wish to create a `.gitignore` file
1. Autograder expected output
    ```
    $ grade test -p lab07
    . start(1/1) index(49/49) not-found(49/49) stop(1/1) 100/100
    ```
