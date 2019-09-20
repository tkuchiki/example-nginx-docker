# try_files

## upstream / proxy keepalive is not configure

```
$ make bench1
docker-compose run bench -n 1000000 http://nginx1/1.jpg
Starting try_files_nginx3_1 ... done
Starting try_files_nginx2_1 ... done
Starting try_files_nginx1_1 ... done

Summary:
  Total:        138.9361 secs
  Slowest:      1.1371 secs
  Fastest:      0.0002 secs
  Average:      0.0069 secs
  Requests/sec: 7197.5549

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.000 [1]     |
  0.114 [999816]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.228 [124]   |
  0.341 [8]     |
  0.455 [0]     |
  0.569 [0]     |
  0.682 [0]     |
  0.796 [0]     |
  0.910 [0]     |
  1.023 [50]    |
  1.137 [1]     |


Latency distribution:
  10% in 0.0031 secs
  25% in 0.0047 secs
  50% in 0.0070 secs
  75% in 0.0084 secs
  90% in 0.0100 secs
  95% in 0.0114 secs
  99% in 0.0159 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0002 secs, 1.1371 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0572 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0479 secs
  resp wait:    0.0027 secs, 0.0001 secs, 0.9305 secs
  resp read:    0.0021 secs, 0.0000 secs, 0.0421 secs

Status code distribution:
  [200] 1000000 responses
```

```
$ make bench2
docker-compose run bench -n 1000000 http://nginx1/2.jpg
Starting try_files_nginx3_1 ... done
Starting try_files_nginx2_1 ... done
Starting try_files_nginx1_1 ... done

Summary:
  Total:        314.9103 secs
  Slowest:      0.1885 secs
  Fastest:      0.0008 secs
  Average:      0.0157 secs
  Requests/sec: 3175.5073

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.020 [822675]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.038 [176398]        |■■■■■■■■■
  0.057 [688]   |
  0.076 [140]   |
  0.095 [58]    |
  0.113 [17]    |
  0.132 [9]     |
  0.151 [6]     |
  0.170 [6]     |
  0.188 [2]     |


Latency distribution:
  10% in 0.0116 secs
  25% in 0.0126 secs
  50% in 0.0144 secs
  75% in 0.0181 secs
  90% in 0.0218 secs
  95% in 0.0242 secs
  99% in 0.0290 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0008 secs, 0.1885 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0736 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0225 secs
  resp wait:    0.0150 secs, 0.0004 secs, 0.1873 secs
  resp read:    0.0003 secs, 0.0000 secs, 0.0369 secs

Status code distribution:
  [200] 1000000 responses
```

```
$ make bench3
docker-compose run bench -n 1000000 http://nginx1/3.jpg
Starting try_files_nginx3_1 ... done
Starting try_files_nginx2_1 ... done
Starting try_files_nginx1_1 ... done

Summary:
  Total:        450.2613 secs
  Slowest:      0.7941 secs
  Fastest:      0.0011 secs
  Average:      0.0225 secs
  Requests/sec: 2220.9325

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.080 [999873]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.160 [26]    |
  0.239 [0]     |
  0.318 [0]     |
  0.398 [0]     |
  0.477 [0]     |
  0.556 [0]     |
  0.636 [0]     |
  0.715 [0]     |
  0.794 [100]   |


Latency distribution:
  10% in 0.0172 secs
  25% in 0.0187 secs
  50% in 0.0207 secs
  75% in 0.0250 secs
  90% in 0.0307 secs
  95% in 0.0339 secs
  99% in 0.0403 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0011 secs, 0.7941 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0348 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0466 secs
  resp wait:    0.0220 secs, 0.0009 secs, 0.7932 secs
  resp read:    0.0002 secs, 0.0000 secs, 0.0406 secs

Status code distribution:
  [200] 1000000 responses
```

## upstream / proxy keepalive is configured

```
$ make bench2
docker-compose run bench -n 1000000 http://nginx1/2.jpg
Starting try_files_nginx3_1 ... done
Starting try_files_nginx2_1 ... done
Starting try_files_nginx1_1 ... done

Summary:
  Total:        172.9297 secs
  Slowest:      0.8798 secs
  Fastest:      0.0004 secs
  Average:      0.0086 secs
  Requests/sec: 5782.6973

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.000 [1]     |
  0.088 [999372]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.176 [564]   |
  0.264 [13]    |
  0.352 [0]     |
  0.440 [0]     |
  0.528 [0]     |
  0.616 [0]     |
  0.704 [0]     |
  0.792 [0]     |
  0.880 [50]    |


Latency distribution:
  10% in 0.0044 secs
  25% in 0.0057 secs
  50% in 0.0075 secs
  75% in 0.0107 secs
  90% in 0.0136 secs
  95% in 0.0153 secs
  99% in 0.0215 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0004 secs, 0.8798 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 0.0291 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0636 secs
  resp wait:    0.0064 secs, 0.0002 secs, 0.8796 secs
  resp read:    0.0011 secs, 0.0000 secs, 0.0475 secs

Status code distribution:
  [200] 1000000 responses
```

```
$ make bench3
docker-compose run bench -n 1000000 http://nginx1/3.jpg
Starting try_files_nginx3_1 ... done
Starting try_files_nginx2_1 ... done
Starting try_files_nginx1_1 ... done

Summary:
  Total:        223.1823 secs
  Slowest:      1.0131 secs
  Fastest:      0.0005 secs
  Average:      0.0111 secs
  Requests/sec: 4480.6413

  Total data:   35588000000 bytes
  Size/request: 35588 bytes

Response time histogram:
  0.001 [1]     |
  0.102 [999770]        |■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■
  0.203 [179]   |
  0.304 [0]     |
  0.406 [0]     |
  0.507 [0]     |
  0.608 [0]     |
  0.709 [0]     |
  0.811 [0]     |
  0.912 [0]     |
  1.013 [50]    |


Latency distribution:
  10% in 0.0053 secs
  25% in 0.0072 secs
  50% in 0.0101 secs
  75% in 0.0140 secs
  90% in 0.0174 secs
  95% in 0.0202 secs
  99% in 0.0277 secs

Details (average, fastest, slowest):
  DNS+dialup:   0.0000 secs, 0.0005 secs, 1.0131 secs
  DNS-lookup:   0.0000 secs, 0.0000 secs, 1.0047 secs
  req write:    0.0000 secs, 0.0000 secs, 0.0648 secs
  resp wait:    0.0093 secs, 0.0004 secs, 1.0100 secs
  resp read:    0.0010 secs, 0.0000 secs, 0.0697 secs

Status code distribution:
  [200] 1000000 responses
```
