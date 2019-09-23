# redis

## no keepalived (redis / http)

```
$ make bench2
docker-compose run bench -n 1000000 http://nginx1/2.jpg
Starting redis_redis_1 ... done
Starting redis_nginx3_1 ... done
Starting redis_nginx2_1 ... done
Starting redis_nginx1_1 ... done

Summary:
  Total:        531.4550 secs
  Slowest:      0.1344 secs
  Fastest:      0.0010 secs
  Average:      0.0265 secs
  Requests/sec: 1881.6270

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.014 [1035]  |
  0.028 [694007]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.041 [286983]        |■■■■■■■■■■■■■■■■■
  0.054 [17497] |■
  0.068 [364]   |
  0.081 [60]    |
  0.094 [27]    |
  0.108 [9]     |
  0.121 [9]     |
  0.134 [8]     |


Latency distribution:
  10% in 0.0217 secs
  25% in 0.0230 secs
  50% in 0.0249 secs
  75% in 0.0289 secs
  90% in 0.0343 secs
  95% in 0.0373 secs
  99% in 0.0430 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0010 secs, 0.1344 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0398 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0175 secs
  resp wait:    0.0262 secs, 0.0009 secs, 0.1330 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.0351 secs

Status code distribution:
  [200] 1000000 responses
```

```
$ make bench3
docker-compose run bench -n 1000000 http://nginx1/3.jpg
Starting redis_redis_1 ... done
Starting redis_nginx3_1 ... done
Starting redis_nginx2_1 ... done
Starting redis_nginx1_1 ... done

Summary:
  Total:        553.9880 secs
  Slowest:      0.4661 secs
  Fastest:      0.0013 secs
  Average:      0.0277 secs
  Requests/sec: 1805.0932

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.048 [994838]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.094 [5054]  |
  0.141 [54]    |
  0.187 [3]     |
  0.234 [0]     |
  0.280 [0]     |
  0.327 [0]     |
  0.373 [0]     |
  0.420 [0]     |
  0.466 [50]    |


Latency distribution:
  10% in 0.0223 secs
  25% in 0.0237 secs
  50% in 0.0258 secs
  75% in 0.0305 secs
  90% in 0.0359 secs
  95% in 0.0391 secs
  99% in 0.0453 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0013 secs, 0.4661 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0369 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0182 secs
  resp wait:    0.0273 secs, 0.0010 secs, 0.4588 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.4376 secs

Status code distribution:
  [200] 1000000 responses
```

## keepalive (redis)

```
$ make bench3
docker-compose run bench -n 1000000 http://nginx1/3.jpg
Starting redis_redis_1 ... done
Starting redis_nginx3_1 ... done
Starting redis_nginx2_1 ... done
Starting redis_nginx1_1 ... done

Summary:
  Total:        427.3972 secs
  Slowest:      1.0096 secs
  Fastest:      0.0011 secs
  Average:      0.0213 secs
  Requests/sec: 2339.7438

  Total data:   35586265155 bytes
  Size/request: 35586 bytes

Response time histogram:
  0.001 [1]     |
  0.102 [999814]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.203 [81]    |
  0.304 [4]     |
  0.404 [0]     |
  0.505 [0]     |
  0.606 [0]     |
  0.707 [0]     |
  0.808 [50]    |
  0.909 [0]     |
  1.010 [50]    |


Latency distribution:
  10% in 0.0159 secs
  25% in 0.0173 secs
  50% in 0.0200 secs
  75% in 0.0244 secs
  90% in 0.0285 secs
  95% in 0.0310 secs
  99% in 0.0366 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0011 secs, 1.0096 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0611 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0329 secs
  resp wait:    0.0208 secs, 0.0008 secs, 1.0095 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0348 secs

Status code distribution:
  [200] 999951 responses
  [500] 49 responses
```

## keepalive (redis / http)

```
$ make bench3
docker-compose run bench -n 1000000 http://nginx1/3.jpg
Starting redis_redis_1 ... done
Starting redis_nginx3_1 ... done
Starting redis_nginx2_1 ... done
Starting redis_nginx1_1 ... done

Summary:
  Total:        289.5591 secs
  Slowest:      0.2987 secs
  Fastest:      0.0007 secs
  Average:      0.0144 secs
  Requests/sec: 3453.5267

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.030 [977724]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.060 [16304] |■
  0.090 [3467]  |
  0.120 [1515]  |
  0.150 [608]   |
  0.180 [242]   |
  0.209 [101]   |
  0.239 [23]    |
  0.269 [10]    |
  0.299 [5]     |


Latency distribution:
  10% in 0.0085 secs
  25% in 0.0104 secs
  50% in 0.0127 secs
  75% in 0.0165 secs
  90% in 0.0209 secs
  95% in 0.0246 secs
  99% in 0.0438 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0007 secs, 0.2987 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0751 secs
  req write:    0.0001 secs, 0.0000 secs, 0.0366 secs
  resp wait:    0.0120 secs, 0.0005 secs, 0.2986 secs
  resp read:    0.0012 secs, 0.0000 secs, 0.0437 secs

Status code distribution:
  [200] 1000000 responses
```
