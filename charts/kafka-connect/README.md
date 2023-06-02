# Kafka Connect UI

This chart bootstraps a deployment of a Confluent Kafka Connect.

## Introduction

Kafka Connect is a tool for scalably and reliably streaming data between Apache Kafka® and other data systems. It makes it simple to quickly define connectors that move large data sets in and out of Kafka. Kafka Connect can ingest entire databases or collect metrics from all your application servers into Kafka topics, making the data available for stream processing with low latency. An export connector can deliver data from Kafka topics into secondary indexes like Elasticsearch, or into batch systems–such as Hadoop for offline analysis.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add rdomenzain https://rdomenzain.github.io/helm-chart
$ helm install --name my-release rdomenzain/kafka-connect
```

The command deploys Kafka Connect on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.


## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Kafka Connect chart and their default values.

| Parameter         | Description                           | Default   |
| ----------------- | ------------------------------------- | --------- |
| `replicaCount`    | The number of Kafka Connect Servers.  | `1`       |
| `groupId`    | Group Id  | `kafka-connect`       |

### Image

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `image` | Docker Image of Confluent Kafka Connect. | `confluentinc/cp-kafka-connect` |
| `imageTag` | Docker Image Tag of Confluent Kafka Connect. | `7.4.0` |
| `imagePullPolicy` | Docker Image Tag of Confluent Kafka Connect. | `IfNotPresent` |
| `imagePullSecrets` | Secrets to be used for private registries. | see [values.yaml](values.yaml) for details |

### Port

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `servicePort` | The port on which the Kafka Connect will be available and serving requests. | `8083` |

### Kafka Connect Worker Configurations

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `configurationOverrides` | Kafka Connect [configuration](https://docs.confluent.io/current/connect/references/allconfigs.html) overrides in the dictionary format. | see [values.yaml](values.yaml) for details |
| `customEnv` | Custom environmental variables | `{}` |

### Volumes

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `volumes` | Volumes for connect-server container | see [values.yaml](values.yaml) for details |
| `volumeMounts` | Volume mounts for connect-server container | see [values.yaml](values.yaml) for details |

### Secrets

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `secrets` | Secret with one or more `key:value` pairs | see [values.yaml](values.yaml) for details |

### Kafka Connect JVM Heap Options

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `heapOptions` | The JVM Heap Options for Kafka Connect | `"-Xms512M -Xmx512M"` |

### Resources

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `resources.requests.cpu` | The amount of CPU to request. | see [values.yaml](values.yaml) for details |
| `resources.requests.memory` | The amount of memory to request. | see [values.yaml](values.yaml) for details |
| `resources.requests.limit` | The upper limit CPU usage for a Kafka Connect Pod. | see [values.yaml](values.yaml) for details |
| `resources.requests.limit` | The upper limit memory usage for a Kafka Connect Pod. | see [values.yaml](values.yaml) for details |

### Annotations

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `podAnnotations` | Map of custom annotations to attach to the pod spec. | `{}` |

### JMX Configuration

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `jmx.port` | The jmx port which JMX style metrics are exposed. | `5555` |

### Prometheus JMX Exporter Configuration

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `prometheus.jmx.enabled` | Whether or not to install Prometheus JMX Exporter as a sidecar container and expose JMX metrics to Prometheus. | `true` |
| `prometheus.jmx.image` | Docker Image for Prometheus JMX Exporter container. | `solsson/kafka-prometheus-jmx-exporter@sha256` |
| `prometheus.jmx.imageTag` | Docker Image Tag for Prometheus JMX Exporter container. | `6f82e2b0464f50da8104acd7363fb9b995001ddff77d248379f8788e78946143` |
| `prometheus.jmx.imagePullPolicy` | Docker Image Pull Policy for Prometheus JMX Exporter container. | `IfNotPresent` |
| `prometheus.jmx.port` | JMX Exporter Port which exposes metrics in Prometheus format for scraping. | `5556` |
| `prometheus.jmx.resources` | JMX Exporter resources configuration. | see [values.yaml](values.yaml) for details |

### Running Custom Scripts

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `customEnv.CUSTOM_SCRIPT_PATH` | Path to external bash script to run inside the container | see [values.yaml](values.yaml) for details |
| `livenessProbe` | Requirement of `livenessProbe` depends on the custom script to be run  | see [values.yaml](values.yaml) for details |

### Deployment Topology

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `nodeSelector` | Dictionary containing key-value-pairs to match labels on nodes. When defined pods will only be scheduled on nodes, that have each of the indicated key-value pairs as labels. Further information can be found in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) | `{}`
| `tolerations`| Array containing taint references. When defined, pods can run on nodes, which would otherwise deny scheduling. Further information can be found in the [Kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/) | `{}`

## Dependencies

### Kafka

| Parameter | Description | Default |
| --------- | ----------- | ------- |
| `kafka.bootstrapServers` | Bootstrap Servers for Kafka Connect | `""` |
| `kafka.kafkaSchemaRegistry.url` | Kafka Schema Registry | `""` |

The above parameters map to the env variables defined in [kafka-connect-ui](https://github.com/lensesio/kafka-connect-ui).
