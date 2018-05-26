# curl

issues a GET request to substack and prints the body.

`$ curl -s http://substack.net`

(The -s gets rid of annoying progress output.)

To see just the headers, use `-I`:

`$ curl -I -s http://substack.net`

Use `-X` to set the http verb (POST) and `-d` to set form parameters:
```
$ curl -X POST http://localhost:5000 -d title=whatever \
-d date=1421044443 -d body='beep boop!'
```

Use `-H` to set header:
```
$ curl -X POST http://localhost:5000 -d title=whatever \
-d date=1421044443 -d body='beep boop!' \
-H cool:beans
```
