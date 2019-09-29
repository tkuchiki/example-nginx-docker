# gzip

## no gzipped

```
$ make curl
curl -I 127.0.0.1:33009/test.json
HTTP/1.1 200 OK
Server: nginx/1.15.12
Date: Sun, 29 Sep 2019 05:16:09 GMT
Content-Type: application/json
Content-Length: 149022
Last-Modified: Sun, 29 Sep 2019 04:15:31 GMT
Connection: keep-alive
ETag: "5d902fe3-2461e"
Accept-Ranges: bytes
```

## gzipped

```
$ make curl_gzipped
curl -H "Accept-Encoding: gzip" -I 127.0.0.1:33009/test.json
HTTP/1.1 200 OK
Server: nginx/1.15.12
Date: Sun, 29 Sep 2019 05:16:16 GMT
Content-Type: application/json
Content-Length: 32906
Last-Modified: Sun, 29 Sep 2019 04:55:46 GMT
Connection: keep-alive
ETag: "5d903952-808a"
Content-Encoding: gzip
```
