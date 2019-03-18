### STEP 1

#### run `backend-service-demo`

```
java -Xms4g -Xmx4g -XX:+UseG1GC backend-service-demo/target/backend-service-demo.jar
```

### STEP 2

#### run `gateway-demo`

```
java -Xms4g -Xmx4g -XX:+UseG1GC backend-service-demo/target/gateway-demo.jar
```

### STEP 3

#### benchmark with `wrk`

* test response with 100 and 10000 characters

![](https://github.com/maoyunfei/gateway-performance-test/blob/master/screenshot/pic1.jpg?raw=true)

* test response with 30000 characters

![](https://github.com/maoyunfei/gateway-performance-test/blob/master/screenshot/pic2.jpg?raw=true)

* test response with 50000 characters

![](https://github.com/maoyunfei/gateway-performance-test/blob/master/screenshot/pic3.jpg?raw=true)

* more test with proxy

![](https://github.com/maoyunfei/gateway-performance-test/blob/master/screenshot/pic4.jpg?raw=true)
