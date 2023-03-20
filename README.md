 boot-opentelemetry-tempo-loki-otel-tempo-prometheus-grafana

# 🚀 Project demonstrating Complete Observability Stack utilizing Prometheus, Loki (For distributed logging), Tempo (For Distributed tracing, this basically uses Jaeger Internally), Grafana for Java/spring based applications (With OpenTelemetry auto / manual Instrumentation) involving multiple microservices with DB interactions 🚀

https://github.com/coding-to-music/boot-opentelemetry-tempo-loki-otel-tempo-prometheus-grafana

https://reachmnadeem.wordpress.com/2021/03/04/observability-for-java-spring-based-applications-using-opentelemetry/

From / By 

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/boot-opentelemetry-tempo-loki-otel-tempo-prometheus-grafana.git
git push -u origin main
```

# Project Demonstrating Observability For Java Spring Applications

This project demonstrates Observability using:

* [Prometheus](https://prometheus.io/) for monitoring and alerting
* [Loki](https://grafana.com/oss/loki/) for Distributed Logging
* [Tempo](https://grafana.com/oss/tempo/) for Distributed Tracing
* [Grafana](https://grafana.com/) for visualization

And basically integrates the following

* [Opentelemetry](https://opentelemetry.io/)
* [Grafana Tempo](https://grafana.com/oss/tempo/) Which internally uses [Jaeger](https://www.jaegertracing.io/)
* [Spring Boot Project](https://spring.io/projects/spring-boot)


# Running

Execute the following on root folder

````bash
mvn clean package docker:build
````

Images

````bash
docker image ls | grep mnadeem

````


```bash
REPOSITORY                          TAG              IMAGE ID       CREATED          SIZE
mnadeem/boot-otel-tempo-provider1   0.0.1-SNAPSHOT   d16f96c59536   29 seconds ago   168MB
mnadeem/boot-otel-tempo-api         0.0.1-SNAPSHOT   8324fcedb409   33 seconds ago   148MB
mnadeem/boot-otel-tempo-docker      0.0.1-SNAPSHOT   dc12190d9235   57 seconds ago   129MB
mnadeem/boot-otel-tempo-docker      latest           dc12190d9235   57 seconds ago   129MB

And then either `docker compose` or `docker stack`

## Docker Compose



````bash
docker-compose up
````

## Docker Stack

````bash
docker swarm init
docker stack deploy --compose-file docker-compose.yaml trace
docker stack services trace
docker stack rm trace

docker stack ls
````

```bash
docker stack services trace
```

Output

```
ID             NAME                              MODE         REPLICAS   IMAGE                                              PORTS
1xzuq25hlowj   trace_boot-otel-tempo-api         replicated   0/1        mnadeem/boot-otel-tempo-api:0.0.1-SNAPSHOT         *:8080->8080/tcp
0nwf98b4vp3q   trace_boot-otel-tempo-provider1   replicated   0/1        mnadeem/boot-otel-tempo-provider1:0.0.1-SNAPSHOT   *:8090->8090/tcp
g1x9bo8vusot   trace_grafana                     replicated   0/1        grafana/grafana:latest                             *:3000->3000/tcp
4g7ikj69c2rf   trace_loki                        replicated   0/1        grafana/loki:2.2.0                                 *:3101->3100/tcp
la4g6cptmczx   trace_pgadmin                     replicated   1/1        dpage/pgadmin4:latest                              *:7070->80/tcp
adbo9s3l5lry   trace_prometheus                  replicated   1/1        prom/prometheus:latest                             *:9090->9090/tcp
mumkw4pcm3qr   trace_promtail                    replicated   0/1        grafana/promtail:2.2.0                             
n0la3spu0gd1   trace_provider1-db                replicated   0/1        postgres:latest                                    *:5432->5432/tcp
wuh6o3ptypmz   trace_tempo                       replicated   0/1        grafana/tempo:0.7.0                                *:3102->3100/tcp, *:14250->14250/tcp, *:14268->14268/tcp, *:55680->55680/tcp
nw5sazythb7i   trace_tempo-query                 replicated   1/1        grafana/tempo-query:0.7.0                          *:16686->16686/tcp
mxvkb23d3g9g   trace_volume_exporter             replicated   0/1        mnadeem/volume_exporter:latest                     *:9889->9888/tcp
```

# Variations 

There are two variations **basic** and **complex**, both version have support for `0.15.0`, `0.16.0` and `0.17.0` in its own branches.

## Basic

Multiple micro-services with **db** and **rest** interactions

## Complex

Multiple micro-services with **db**, **MQ (Rabbit)**, **redis** and **rest** interactions

# Tracing

[Access the endpoint](http://localhost:8080/flights)

![](docs/img/access-flights.png)

View the log and trace in [Grafana](http://localhost:3000/explore)

![](docs/img/grafana-loki-trace.png)


Get the trace information Using **[Jaeger](http://localhost:16686/search)** as well

**Basic Trace**

![](docs/img/jaeger-trace.png)

**Complex Trace**

![](docs/img/jaeger-trace-complex.png)


# Prometheus Metrics

View the metrics in [prometheus](http://localhost:9090/graph?g0.expr=&g0.tab=1&g0.stacked=0&g0.range_input=1h)

![](docs/img/prometheus-metrics.png)

You can view it in [Grafana](http://localhost:3000/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22Prometheus%22,%7B%22expr%22:%22http_server_requests_seconds_count%22,%22requestId%22:%22Q-0a6b4a46-2eeb-428a-b98d-0170a5fe4900-0A%22%7D%5D) as well

![](docs/img/grafana-prom-metrics.png)


# Connecting To PostgreSQL DB

[Connect](http://localhost:7070/login?next=%2F)

![](docs/img/pgAdminlogin.png)

![](docs/img/pgAdmingServer.png)

![](docs/img/pgAdminDb.png)


# Credits

* [otel-demo](https://github.com/williewheeler/otel-demo)
* [java-agent-spring-boot-example](https://github.com/objectiser/java-agent-spring-boot-example)


# Also See
* [Nodejs Opentelemetry Tempo](https://github.com/mnadeem/nodejs-opentelemetry-tempo)
