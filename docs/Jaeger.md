## Jaeger

<br>
<div style="text-align:center" align="center"><img src ="resources/jaeger-vector.svg" width="100"/></div>
<br>

[Jaeger](https://github.com/jaegertracing/jaeger) is an open source distributed tracing system. Jaeger tracer is built using OpenTracing compatible data model. [Opentracing](http://opentracing.io/) is a vendor-neutral open standard for distributed tracing. JP4Agent uses its C++ client library to integrate with Jaeger. Use of Jaeger for tracing is optional – it can be disabled for setups where Jaeger collector sub-system cannot be made available for collecting the traces.


### Jaeger Integration

<br>
<div style="text-align:center" align="center"><img src ="resources/JaegerIntegration.png" width="600"/></div>
<br>
<br>

### STEP 1: Launch the Jaeger backend using All-in-one Docker image on a server reachable from JP4Agent.
```
docker run -d -e COLLECTOR_ZIPKIN_HTTP_PORT=9411 -p5775:5775/udp -p6831:6831/udp -p6832:6832/udp \
  -p5778:5778 -p16686:16686 -p14268:14268 -p9411:9411 jaegertracing/all-in-one:latest
```

### STEP 2: Update JP4Agent/src/config.yaml with the IP address of the server running Jaeger backend
```
e.g. if Jaeger backend is running on 120.54.23.21

localAgentHostPort: 120.54.23.21:6831

hostPort: 120.54.23.21:5778
```

### STEP3: Launch Docker GUI in browser using IP address of Jaeger backend
```
E.g. if Jaeger backend IP is 120.54.23.21

http://120.54.23.21:16686

Alternately, if browser is running on the same host as Jaeger back end use

http://127.0.0.1:16686
```

### NOTES
```
    1. Jaeger backend should be run on a host different from the one running vMX
    2. Jaeger Backend must be started prior to launching JP4Agent.
    3. Ensure that date and time on the servers running JP4Agent and Jaeger backend are in synch.
    4. If you do not intend to run Jaeger, specify Jaeger config file as  "" in
       JP4Agent/config/jp4agent-cfg.json as below:
       "jaeger-config-file"   : ""
```
