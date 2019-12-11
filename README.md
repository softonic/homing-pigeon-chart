# Homing Pigeon

Helm chart for https://github.com/softonic/homing-pigeon

[![Latest Version](https://img.shields.io/github/release/softonic/homing-pigeon-chart.svg)](https://github.com/softonic/homing-pigeon-chart/releases)
[![Software License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/softonic/homing-pigeon-chart.svg)](http://isitmaintained.com/project/softonic/homing-pigeon-chart "Average time to resolve an issue")
![GitHub issues](https://img.shields.io/github/issues-raw/softonic/homing-pigeon-chart)

### Overview

| Parameter                                           | Description                                                                               | Default                            |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------- |
| `image.repository`                                  | Image repository                                                                          | `softonic/homing-pigeon`           |
| `image.tag`                                         | Tag used for the image                                                                    | `0.1.0`                            |
| `image.pullPolicy`                                  | Image pull policy                                                                         | `IfNotPresent`                     |
| `resources`                                         | Resources policy                                                                          | `{}`                               |
| `updateStrategy`                                    | Update strategy for statefulset                                                           | `null`                             |
| `nodeSelector`                                      | Node Selector for homing pigeon deployment                                                | `{}`                               |
| `tolerations`                                       | Tolerations for homing pigeon deployment                                                  | `[]`                               |
| `affinity`                                          | Affinity for homing pigeon deployment                                                     | `{}`                               |
| `initContainers`                                    | List of init containers                                                                   | `[]`                               |
| `extraContainers`                                   | List of extra containers to add to homing pigeon pod                                      | `[]`                               |
| `nameOverride`                                      | Override name of chart                                                                    | `""`                               |
| `fullnameOverride`                                  | Override full name of chart                                                               | `""`                               |
| `replicaCount`                                      | Number of replicas for homing pigeon deployment                                           | `1`                                |
| `consumerId`                                        | Define CONSUMER_ID env var. It affects `queueName`                                        | `null`                             |
| `messageBufferLen`                                  | Buffer length for write buffer                                                            | `400`                              |
| `ackBufferLen`                                      | Buffer length for acks                                                                    | `200`                              |
| `caCerts`                                           | List of CA certs with `name` being an identifier, and `cert` the certificate in base64    | `null`                             |
| `reader.rabbitmq.enabled`                           | Enable RabbitMQ reader                                                                    | `false`                            |
| `reader.rabbitmq.consumerName`                      | Consumer identifier label                                                                 | `""`                               |
| `reader.rabbitmq.url`                               | RabbitMQ url                                                                              | `""`                               |
| `reader.rabbitmq.caCertName`                        | Enable SSL for RabbitMQ                                                                   | `""`                               |
| `reader.rabbitmq.deadLettersExchangeName`           | RabbitMQ reader dead letters exchange name (where unacked and unroutable messsages go to) | `""`                               |
| `reader.rabbitmq.deadLettersQueueName`              | RabbitMQ reader dead letters queue name                                                   | `""`                               |
| `reader.rabbitmq.exchangeName`                      | RabbitMQ reader exchange name                                                             | `""`                               |
| `reader.rabbitmq.exchangeType`                      | RabbitMQ reader exchange type                                                             | `""`                               |
| `reader.rabbitmq.exchangeInternal`                  | Whether RabbitMQ exchange is internal or not                                              | `"false"`                          |
| `reader.rabbitmq.outerExchangeName`                 | RabbitMQ reader outer exchange name                                                       | `""`                               |
| `reader.rabbitmq.outerExchangeType`                 | RabbitMQ reader outer exchange type                                                       | `""`                               |
| `reader.rabbitmq.outerExchangeBindingKey`           | RabbitMQ reader binding key for outer exchange                                            | `""`                               |
| `reader.rabbitmq.queueName`                         | RabbitMQ reader queue name. It supports templating.                                       | `""`                               |
| `reader.rabbitmq.qos.prefetchCount`                 | RabbitMQ QoS prefetch count                                                               | `0`                                |
| `writer.elasticsearch.enabled`                      | elasticsearch writer enabled                                                              | `false`                            |
| `writer.elasticsearch.host`                         | elasticsearch writer host                                                                 | `""`                               |
| `writer.elasticsearch.flushMaxSize`                 | elasticsearch writer flush max size for bulk writes                                       | `100`                              |
| `writer.elasticsearch.flushMaxIntervalMs`           | elasticsearch writer flush max interval for bulk writes in ms                             | `5000`                             |
| `middlewares[*].name`                               | middleware name                                                                           | `null`                             |
| `middlewares[*].repository`                         | middleware image repository                                                               | `null`                             |
| `middlewares[*].tag`                                | middleware image tag                                                                      | `null`                             |
| `middlewares[*].pullPolicy`                         | middleware image pull policy                                                              | `IfNotPresent`                     |

QueueName templating available variables:

| Name       | Description                                                                                                                                               |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ConsumerId | Everything after the last `-` in the hostname by default. If no `-` are present, the whole hostname is used. Can be overriden with `CONSUMER_ID` env var. |

### Middleware

You can define middlewares using the `middlewares` key. The middlewares will be concatenated in the same order than declared
in the yaml.

### Usage

```
helm repo add softonic https://charts.softonic.io
helm upgrade homing-pigeon --install softonic/homing-pigeon
```
