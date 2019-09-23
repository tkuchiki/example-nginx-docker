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
