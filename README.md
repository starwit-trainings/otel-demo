# Open Telemetry Test Setup

This repository is a minimal setup for an Open Telemetry collecting backend. NOTE: This is by no means intended to be used in a productive scenario! In fact this is an excerpt of Open Telemetry's fantastic microservice example which is documented here: https://opentelemetry.io/docs/demo/docker-deployment/

## Structure
This setup consists of the following components:
| Component                | Port/Path          |
| ------------------------ | ------------------ |
| Opentelemetry Collector  | 4317/4318          |
| Grafana                  | host:28080/grafana |
| Prometheus               | host/prometheus/   |
| OpenSearch               | host:9200          |
| Envoy Proxy              | host:28080         |

## Usage

Setup is based on Docker compose and so running example works like this:
```bash
    docker compose -f docker-compose.yaml up
```
Images for proxy and Grafana are going to be build before starting. Proxy contains config to reach all components and Grafana image is build, to create an image, that can run without internet access.

You can find all config files in [this folder](otel-configs/). If you just want to run setup in this repo, then the most important config is found in file [.env](./.env). 

If setup is running, you can start collecting data. The following subsections show you examples how to do this.

### Example with Java

Main thing you need to do, is to start Java with parameter javaagent like so:
```
    -javaagent:./opentelemetry-javaagent.jar -Dotel.service.name=service-name
``` 
Obviously you need to provide the Open Telemetry java library. Latest release can be found here:
https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases

If you want to package your Java in a Docker image (and you should), here is an example:
https://github.com/starwit-trainings/microservice-compose/tree/main/service-composition-otel/infoservice

### Example with Python
Open Telemetry can be used with many languages and here is an example, how to integrate it into a Python Rest service:
https://github.com/starwit-trainings/logo-microservice-example/tree/main/logo-service-otel 
