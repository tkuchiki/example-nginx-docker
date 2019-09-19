# rate limit

## Request from multiple sources

### No rate limit

```console
# terminal 1
$ docker-compose run bench -c 1 -q 5 -n 100 http://nginx/rate_limit
Starting example-nginx-docker_nginx_1 ... done

Summary:
  Total:        20.0014 secs
  Slowest:      0.0053 secs
  Fastest:      0.0005 secs
  Average:      0.0011 secs
  Requests/sec: 4.9996

  Total data:   61200 bytes
  Size/request: 612 bytes

Response time histogram:
  0.001 [1]     |■
  0.001 [51]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.001 [41]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.002 [4]     |■■■
  0.002 [2]     |■■
  0.003 [0]     |
  0.003 [0]     |
  0.004 [0]     |
  0.004 [0]     |
  0.005 [0]     |
  0.005 [1]     |■


Latency distribution:
  10% in 0.0008 secs
  25% in 0.0009 secs
  50% in 0.0010 secs
  75% in 0.0012 secs
  90% in 0.0014 secs
  95% in 0.0016 secs
  99% in 0.0053 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 0.0053 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0022 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0003 secs
  resp wait:    0.0006 secs, 0.0003 secs, 0.0010 secs
  resp read:    0.0002 secs, 0.0001 secs, 0.0009 secs

Status code distribution:
  [200] 100 responses

# terminal 2
$ docker-compose run bench -c 1 -q 5 -n 100 http://nginx/rate_limit
Starting example-nginx-docker_nginx_1 ... done

Summary:
  Total:        20.0015 secs
  Slowest:      0.0044 secs
  Fastest:      0.0005 secs
  Average:      0.0011 secs
  Requests/sec: 4.9996

  Total data:   61200 bytes
  Size/request: 612 bytes

Response time histogram:
  0.001 [1]     |■
  0.001 [28]    |■■■■■■■■■■■■■■■■■■■■■■
  0.001 [52]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.002 [13]    |■■■■■■■■■■
  0.002 [2]     |■■
  0.002 [1]     |■
  0.003 [1]     |■
  0.003 [1]     |■
  0.004 [0]     |
  0.004 [0]     |
  0.004 [1]     |■


Latency distribution:
  10% in 0.0007 secs
  25% in 0.0008 secs
  50% in 0.0011 secs
  75% in 0.0012 secs
  90% in 0.0015 secs
  95% in 0.0019 secs
  99% in 0.0044 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 0.0044 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0018 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0003 secs
  resp wait:    0.0006 secs, 0.0002 secs, 0.0026 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.0007 secs

Status code distribution:
  [200] 100 responses
```

### Rate limit (all requests)

```
# terminal 1~4
$ sleep $(awk -v seed="${RANDOM}" 'BEGIN{srand(seed); r=rand(); print r}'); docker-compose run bench -c 1 -q 5 -n 200 http://nginx/rate_limit
```

nginx error log

```
2019/08/26 07:53:36 [error] 7#7: *18 limiting requests, excess: 15.060 by zone "all", client: 172.26.0.5, server: localhost, request: "GET /rate_limit HTTP/1.1", host: "nginx"
```

## Request from single source

### Rate limit (IP base)

```console
$ docker-compose run bench -c 1 -q 10 -n 100 http://nginx/rate_limit
Starting example-nginx-docker_nginx_1 ... done

Summary:
  Total:        10.0013 secs
  Slowest:      0.0029 secs
  Fastest:      0.0005 secs
  Average:      0.0010 secs
  Requests/sec: 9.9987

  Total data:   56480 bytes
  Size/request: 564 bytes

Response time histogram:
  0.000 [1]     |■
  0.001 [25]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.001 [29]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.001 [25]    |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.001 [14]    |■■■■■■■■■■■■■■■■■■■
  0.002 [3]     |■■■■
  0.002 [2]     |■■■
  0.002 [0]     |
  0.002 [0]     |
  0.003 [0]     |
  0.003 [1]     |■


Latency distribution:
  10% in 0.0006 secs
  25% in 0.0007 secs
  50% in 0.0009 secs
  75% in 0.0011 secs
  90% in 0.0014 secs
  95% in 0.0014 secs
  99% in 0.0029 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 0.0029 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0012 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0004 secs
  resp wait:    0.0005 secs, 0.0002 secs, 0.0009 secs
  resp read:    0.0001 secs, 0.0000 secs, 0.0006 secs

Status code distribution:
  [200] 60 responses
  [503] 40 responses
```

nginx error log

```
2019/08/26 07:55:19 [error] 7#7: *20 limiting requests, excess: 5.005 by zone "ip", client: 172.26.0.3, server: localhost, request: "GET /rate_limit HTTP/1.1", host: "nginx"
```
