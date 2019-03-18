### STEP 1

```bash
mvn clean package -DskipTests
```

### STEP 2

#### run `backend-service-demo`

```
java -Xms4g -Xmx4g -XX:+UseG1GC backend-service-demo/target/backend-service-demo.jar
```

### STEP 4

#### run `gateway-demo`

```
java -Xms4g -Xmx4g -XX:+UseG1GC backend-service-demo/target/gateway-demo.jar
```

#### benchmark with `wrk`

#### Test response with 100 characters
```bash
# direct to app
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8081/demo?delay=50&length=128" --latency
Running 30s test @ http://127.0.0.1:8081/demo?delay=50&length=128
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    56.42ms    2.89ms  81.30ms   66.45%
    Req/Sec   213.08     36.63   242.00     82.49%
  Latency Distribution
     50%   56.42ms
     75%   58.35ms
     90%   60.10ms
     99%   63.05ms
  102028 requests in 30.10s, 26.17MB read
Requests/sec:   3389.50
Transfer/sec:      0.87MB

# gateway 
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8082/proxy/demo?delay=50&length=128" --latency
Running 30s test @ http://127.0.0.1:8082/proxy/demo?delay=50&length=128
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    61.90ms    6.45ms 109.22ms   71.10%
    Req/Sec   194.38     28.76   242.00     68.03%
  Latency Distribution
     50%   60.47ms
     75%   65.56ms
     90%   70.90ms
     99%   80.81ms
  93040 requests in 30.10s, 21.74MB read
  Socket errors: connect 0, read 59, write 3, timeout 0
Requests/sec:   3090.91
Transfer/sec:    739.52KB

```

#### Test response with 10240 characters
```bash
# direct to app
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8081/demo?delay=50&length=10240" --latency
Running 30s test @ http://127.0.0.1:8081/demo?delay=50&length=10240
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    58.85ms    3.40ms  74.01ms   67.73%
    Req/Sec   204.10     42.25   242.00     78.71%
  Latency Distribution
     50%   58.75ms
     75%   61.26ms
     90%   63.17ms
     99%   66.95ms
  97722 requests in 30.09s, 0.94GB read
Requests/sec:   3247.59
Transfer/sec:     32.16MB


# gateway
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8082/proxy/demo?delay=50&length=10240" --latency
Running 30s test @ http://127.0.0.1:8082/proxy/demo?delay=50&length=10240
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    67.86ms   13.67ms 187.01ms   83.08%
    Req/Sec   177.29     30.20   242.00     68.16%
  Latency Distribution
     50%   63.91ms
     75%   72.70ms
     90%   85.05ms
     99%  118.82ms
  84882 requests in 30.06s, 838.56MB read
  Socket errors: connect 0, read 33, write 7, timeout 0
Requests/sec:   2824.05
Transfer/sec:     27.90MB

```

#### Test response with 40960 characters

```bash
# direct to app
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8081/demo?delay=50&length=40960" --latency
Running 30s test @ http://127.0.0.1:8081/demo?delay=50&length=40960
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    64.54ms    6.02ms  91.79ms   64.74%
    Req/Sec   185.97     46.01   245.00     51.01%
  Latency Distribution
     50%   65.35ms
     75%   68.80ms
     90%   71.61ms
     99%   78.36ms
  88990 requests in 30.07s, 3.41GB read
Requests/sec:   2958.94
Transfer/sec:    115.99MB



# gateway 
$ wrk -t16 -c200 -d30s "http://127.0.0.1:8082/proxy/demo?delay=50&length=40960" --latency
Running 30s test @ http://127.0.0.1:8082/proxy/demo?delay=50&length=40960
  16 threads and 200 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    77.63ms   15.66ms 298.06ms   70.87%
    Req/Sec   155.60     32.37   242.00     65.12%
  Latency Distribution
     50%   77.54ms
     75%   86.77ms
     90%   95.10ms
     99%  117.32ms
  74348 requests in 30.10s, 2.84GB read
  Socket errors: connect 0, read 72, write 5, timeout 0
Requests/sec:   2470.07
Transfer/sec:     96.77MB


```



