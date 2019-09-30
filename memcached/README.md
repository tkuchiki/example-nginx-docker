# memcached

## no keepalived

```
$ make bench1
docker-compose run bench -n 1000000 http://nginx1/1.jpg
Starting memcached_memcached_1 ... done
Starting memcached_nginx3_1    ... done
Starting memcached_nginx2_1    ... done
Starting memcached_nginx1_1    ... done

Summary:
  Total:        379.1383 secs
  Slowest:      0.5165 secs
  Fastest:      0.0006 secs
  Average:      0.0189 secs
  Requests/sec: 2637.5597

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.052 [999294]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.104 [642]   |
  0.155 [37]    |
  0.207 [18]    |
  0.259 [2]     |
  0.310 [4]     |
  0.362 [0]     |
  0.413 [0]     |
  0.465 [1]     |
  0.517 [1]     |


Latency distribution:
  10% in 0.0154 secs
  25% in 0.0163 secs
  50% in 0.0178 secs
  75% in 0.0204 secs
  90% in 0.0241 secs
  95% in 0.0269 secs
  99% in 0.0335 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0006 secs, 0.5165 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0782 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0157 secs
  resp wait:    0.0184 secs, 0.0004 secs, 0.5160 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0261 secs

Status code distribution:
  [200] 1000000 responses
```

## keepalive

```
$ make bench1
docker-compose run bench -n 1000000 http://nginx1/1.jpg
Starting memcached_memcached_1 ... done
Starting memcached_nginx3_1    ... done
Starting memcached_nginx2_1    ... done
Starting memcached_nginx1_1    ... done

Summary:
  Total:        232.6831 secs
  Slowest:      1.0071 secs
  Fastest:      0.0005 secs
  Average:      0.0116 secs
  Requests/sec: 4297.6906

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.101 [999811]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.202 [127]   |
  0.302 [11]    |
  0.403 [0]     |
  0.504 [0]     |
  0.604 [0]     |
  0.705 [0]     |
  0.806 [0]     |
  0.906 [40]    |
  1.007 [10]    |


Latency distribution:
  10% in 0.0089 secs
  25% in 0.0096 secs
  50% in 0.0107 secs
  75% in 0.0126 secs
  90% in 0.0153 secs
  95% in 0.0173 secs
  99% in 0.0236 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 1.0071 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0189 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0200 secs
  resp wait:    0.0110 secs, 0.0003 secs, 1.0069 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0393 secs

Status code distribution:
  [200] 1000000 responses
```

## keepalive + try_files

### return local file

```
$ make bench2
docker-compose run bench -n 1000000 http://nginx1/2.jpg
Starting memcached_memcached_1 ... done
Starting memcached_nginx3_1    ... done
Starting memcached_nginx2_1    ... done
Starting memcached_nginx1_1    ... done

Summary:
  Total:        147.1304 secs
  Slowest:      0.5397 secs
  Fastest:      0.0002 secs
  Average:      0.0073 secs
  Requests/sec: 6796.6941

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.000 [1]     |
  0.054 [999257]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.108 [505]   |
  0.162 [82]    |
  0.216 [10]    |
  0.270 [17]    |
  0.324 [10]    |
  0.378 [57]    |
  0.432 [11]    |
  0.486 [0]     |
  0.540 [50]    |


Latency distribution:
  10% in 0.0035 secs
  25% in 0.0052 secs
  50% in 0.0074 secs
  75% in 0.0089 secs
  90% in 0.0105 secs
  95% in 0.0119 secs
  99% in 0.0160 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0002 secs, 0.5397 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0754 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0477 secs
  resp wait:    0.0031 secs, 0.0001 secs, 0.5368 secs
  resp read:    0.0022 secs, 0.0000 secs, 0.0387 secs

Status code distribution:
  [200] 1000000 responses
```

### keepalive + try_file

```
$ make bench1
docker-compose run bench -n 1000000 http://nginx1/1.jpg
Starting memcached_memcached_1 ... done
Starting memcached_nginx3_1    ... done
Starting memcached_nginx2_1    ... done
Starting memcached_nginx1_1    ... done

Summary:
  Total:        241.5726 secs
  Slowest:      1.0571 secs
  Fastest:      0.0005 secs
  Average:      0.0120 secs
  Requests/sec: 4139.5426

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.106 [999836]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.212 [59]    |
  0.317 [5]     |
  0.423 [6]     |
  0.529 [8]     |
  0.634 [3]     |
  0.740 [4]     |
  0.846 [3]     |
  0.951 [53]    |
  1.057 [22]    |


Latency distribution:
  10% in 0.0091 secs
  25% in 0.0099 secs
  50% in 0.0110 secs
  75% in 0.0129 secs
  90% in 0.0160 secs
  95% in 0.0185 secs
  99% in 0.0248 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 1.0571 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.8834 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0227 secs
  resp wait:    0.0115 secs, 0.0003 secs, 1.0531 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0609 secs

Status code distribution:
  [200] 1000000 responses
```

## memcached multi hosts

```
$ make bench_multi1
docker-compose run bench -n 1000000 http://nginx1/multi/1.jpg
Starting memcached_memcached1_1 ... done
Starting memcached_memcached2_1 ... done
Starting memcached_memcached3_1 ... done
Starting memcached_nginx3_1     ... done
Starting memcached_nginx2_1     ... done
Starting memcached_nginx1_1     ... done

Summary:
  Total:        302.2624 secs
  Slowest:      1.0277 secs
  Fastest:      0.0006 secs
  Average:      0.0151 secs
  Requests/sec: 3308.3834

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.103 [999872]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.206 [27]    |
  0.309 [0]     |
  0.411 [0]     |
  0.514 [0]     |
  0.617 [0]     |
  0.720 [0]     |
  0.822 [0]     |
  0.925 [50]    |
  1.028 [50]    |


Latency distribution:
  10% in 0.0088 secs
  25% in 0.0106 secs
  50% in 0.0142 secs
  75% in 0.0180 secs
  90% in 0.0215 secs
  95% in 0.0246 secs
  99% in 0.0320 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0006 secs, 1.0277 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0237 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0264 secs
  resp wait:    0.0146 secs, 0.0003 secs, 1.0275 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0405 secs

Status code distribution:
  [200] 1000000 responses
```
```
$ make bench_multi2
docker-compose run bench -n 1000000 http://nginx1/multi/2.jpg
Starting memcached_memcached3_1 ... done
Starting memcached_memcached1_1 ... done
Starting memcached_memcached2_1 ... done
Starting memcached_nginx3_1     ... done
Starting memcached_nginx2_1     ... done
Starting memcached_nginx1_1     ... done

Summary:
  Total:        290.2844 secs
  Slowest:      1.0209 secs
  Fastest:      0.0005 secs
  Average:      0.0145 secs
  Requests/sec: 3444.8981

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.000 [1]     |
  0.103 [999937]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.205 [12]    |
  0.307 [0]     |
  0.409 [0]     |
  0.511 [0]     |
  0.613 [0]     |
  0.715 [0]     |
  0.817 [39]    |
  0.919 [0]     |
  1.021 [11]    |


Latency distribution:
  10% in 0.0086 secs
  25% in 0.0105 secs
  50% in 0.0137 secs
  75% in 0.0173 secs
  90% in 0.0204 secs
  95% in 0.0233 secs
  99% in 0.0301 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 1.0209 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0185 secs
  req write:    0.0000 secs, 0.0000 secs, 0.7690 secs
  resp wait:    0.0140 secs, 0.0003 secs, 1.0176 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.7709 secs

Status code distribution:
  [200] 1000000 responses
```

```
$ make bench_multi3
docker-compose run bench -n 1000000 http://nginx1/multi/3.jpg
Starting memcached_memcached2_1 ... done
Starting memcached_memcached1_1 ... done
Starting memcached_nginx3_1     ... done
Starting memcached_nginx2_1     ... done
Starting memcached_nginx1_1     ... done

Summary:
  Total:        305.1954 secs
  Slowest:      1.0238 secs
  Fastest:      0.0005 secs
  Average:      0.0152 secs
  Requests/sec: 3276.5897

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.000 [1]     |
  0.103 [999823]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.205 [67]    |
  0.307 [5]     |
  0.410 [1]     |
  0.512 [0]     |
  0.614 [3]     |
  0.717 [19]    |
  0.819 [1]     |
  0.921 [77]    |
  1.024 [3]     |


Latency distribution:
  10% in 0.0088 secs
  25% in 0.0110 secs
  50% in 0.0143 secs
  75% in 0.0180 secs
  90% in 0.0218 secs
  95% in 0.0249 secs
  99% in 0.0327 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 1.0238 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.8344 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0149 secs
  resp wait:    0.0147 secs, 0.0003 secs, 1.0237 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.0346 secs

Status code distribution:
  [200] 1000000 responses
```
