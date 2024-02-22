# Kubernetes ReplicaSets

We use ReplicaSets to handle the creation of Pods, instead of manually specifying them. Furthermore, ReplicaSets ensure the lifecycle of pods is handled gracefully, and terminated pods are automatically restarted.

You can test this scenario by issuing `kubectl delete pod webapp-zgqth` and reloading your browser. If you had only one replica defined, you'll notice a brief blip, but the service is restored quickly. In case you had more than one replica defined, then there'll be no outage.

In order to test this theory, we would run ApacheBench for 30 seconds (4 parallel requests, using keepalive, maximum 30 seconds or 100k requests, whichever comes first, aking for compressed pages)

`ab -c 4 -k -s 3 -t 30 -H 'Accept-Encoding: gzip, deflate, sdch' -n 100000 "http://127.0.0.1:30080/"`

and then kill one of the containers:

`kubectl delete pod webapp-q8qkx`

We can now observe how killing of a container affected the responses - only 3 out of 100,000 requests failed - and because we had set the number of replicas to two.

```
This is ApacheBench, Version 2.3 <$Revision: 1903618 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 127.0.0.1 (be patient)
Completed 10000 requests
Completed 20000 requests
Completed 30000 requests
Completed 40000 requests
Completed 50000 requests
Completed 60000 requests
Completed 70000 requests
Completed 80000 requests
Completed 90000 requests
Completed 100000 requests
Finished 100000 requests


Server Software:        nginx/1.14.0
Server Hostname:        127.0.0.1
Server Port:            30080

Document Path:          /
Document Length:        598 bytes

Concurrency Level:      4
Time taken for tests:   11.621 seconds
Complete requests:      100000
Failed requests:        3
   (Connect: 0, Receive: 0, Length: 3, Exceptions: 0)
Keep-Alive requests:    99001
Total transferred:      83592512 bytes
HTML transferred:       59798206 bytes
Requests per second:    8605.16 [#/sec] (mean)
Time per request:       0.465 [ms] (mean)
Time per request:       0.116 [ms] (mean, across all concurrent requests)
Transfer rate:          7024.68 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.0      0       2
Processing:     0    0   0.3      0      10
Waiting:        0    0   0.3      0       8
Total:          0    0   0.3      0      10

Percentage of the requests served within a certain time (ms)
  50%      0
  66%      0
  75%      0
  80%      0
  90%      1
  95%      1
  98%      1
  99%      2
 100%     10 (longest request)
```

After bumping up the number of replicas to 4, we had zero errors on the same benchmark.