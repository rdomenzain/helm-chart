# ksqlDB Server

[ksqlDB](https://ksqldb.io/) is the streaming SQL engine for Apache Kafka. It provides an easy-to-use yet powerful interactive SQL interface for stream processing on Kafka, without the need to write code in a programming language such as Java or Python. ksqlDB is scalable, elastic, fault-tolerant, and it supports a wide range of streaming operations, including data filtering, transformations, aggregations, joins, windowing, and sessionization.

## Introduction

This chart bootstraps a [ksqlDB](https://ksqldb.io/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add rdomenzain https://rdomenzain.github.io/helm-chart
$ helm install --name my-release rdomenzain/ksqldb
```

The command deploys ksqlDB on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Metabase chart and their default values.

### Image and Repository

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| image.registry         | docker.io                        | Registry for the ksqlDB image                         |
| image.repository       | confluentinc/ksqldb-server       | Repository for the ksqlDB image                       |
| image.tag              |                                  | Tag for the ksqlDB image                              |
| image.pullPolicy       | IfNotPresent                     | Image pull policy for the ksqlDB container            |
| imagePullSecrets       | []                               | Image pull secrets for private image repositories     |

### Deployment Name

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| nameOverride           |                                  | Override for the deployment name                      |
| fullnameOverride       |                                  | Override for the full deployment name                 |

### ksqlDB Configuration

| Parameter                          | Default Value        | Description                                           |
|------------------------------------|----------------------|-------------------------------------------------------|
| configurationOverrides             | {}                   | Overrides for ksqlDB server configuration properties  |
| replicaCount                       | 1                    | Number of replicas for ksqlDB deployment              |
| port                               | 8088                 | Port on which ksqlDB server will listen               |
| loggingProcessing.streamAutoCreate | true                 | Automatically create streams in ksqlDB                |
| loggingProcessing.topicAutoCreate  | true                 | Automatically create topics in ksqlDB                 |
| confluentSupportMetricsEnable      | false                | Enable Confluent Support Metrics                      |
| internalTopicReplicas              | 1                    | Number of replicas for internal ksqlDB topics         |

### Ingress Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| ingress.enabled        | false                            | Enable Ingress for ksqlDB server                      |
| ingress.hosts          | []                               | Hosts for Ingress resource                            |
| ingress.path           | /                                | Path for Ingress resource                             |
| ingress.labels         | {}                               | Labels for Ingress resource                           |
| ingress.annotations    | {}                               | Annotations for Ingress resource                      |
| ingress.tls            | []                               | TLS configuration for Ingress resource                |

### ksqlDB Headless Mode Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| queriesFileConfigMap   |                                  | ConfigMap for deploying ksqlDB in headless mode       |

### Kafka Cluster Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| kafka.bootstrapServers | kafka:9092                       | Bootstrap servers for the Kafka cluster               |

### Schema Registry Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| schema-registry.url    | schema-registry:8081             | URL for the Schema Registry                           |

### Kafka Connect Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| kafka-connect.url      | kafka-connect:8083               | URL for Kafka Connect                                 |

### Monitoring Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| jmx.port               | 5555                             | JMX port for ksqlDB monitoring                        |

### Prometheus Exporter Configuration

| Parameter                      | Default Value                                                    | Description                                     |
|--------------------------------|------------------------------------------------------------------|-------------------------------------------------|
| prometheus.jmx.enabled         | true                                                             | Enable Prometheus JMX Exporter                  |
| prometheus.jmx.image           | solsson/kafka-prometheus-jmx-exporter@sha256                     | Prometheus JMX Exporter image                   |
| prometheus.jmx.imageTag        | 6f82e2b0464f50da8104acd7363fb9b995001ddff77d248379f8788e78946143 | Prometheus JMX Exporter image tag               |
| prometheus.jmx.imagePullPolicy | IfNotPresent                                                     | Image pull policy for Prometheus JMX Exporter   |
| prometheus.jmx.port            | 5556                                                             | Prometheus JMX Exporter port                    |
| prometheus.jmx.resources       | {}                                                               | Resources for Prometheus JMX Exporter container |

### Basic Authentication Configuration

| Parameter                     | Default Value              | Description                                           |
|-------------------------------|----------------------------|-------------------------------------------------------|
| basicAuth.enabled             | false                      | Enable basic authentication for ksqlDB server         |
| basicAuth.roles               | ""                         | Roles for basic authentication                        |
| basicAuth.realm               | "KsqlServer-Props"         | Realm for basic authentication                        |
| basicAuth.existingSecretUsers | ""                         | Existing secret for user credentials                  |
| basicAuth.existingSecretJaas  | ""                         | Existing secret for JAAS configuration                |
| basicAuth.skipPaths           | "/,/info,/healthcheck"     | Paths to skip basic authentication                    |

### Liveness and Readiness Probes Configuration

| Parameter                          | Default Value            | Description                                           |
|------------------------------------|--------------------------|-------------------------------------------------------|
| livenessProbe.enabled              | true                     | Enable liveness probe for ksqlDB server               |
| livenessProbe.initialDelaySeconds  | 60                       | Initial delay for liveness probe                      |
| livenessProbe.periodSeconds        | 10                       | Probe period for liveness probe                       |
| livenessProbe.timeoutSeconds       | 30                       | Probe timeout for liveness probe                      |
| livenessProbe.failureThreshold     | 10                       | Failure threshold for liveness probe                  |
| livenessProbe.successThreshold     | 1                        | Success threshold for liveness probe                  |
| readinessProbe.enabled             | true                     | Enable readiness probe for ksqlDB server              |
| readinessProbe.initialDelaySeconds | 60                       | Initial delay for readiness probe                     |
| readinessProbe.periodSeconds       | 10                       | Probe period for readiness probe                      |
| readinessProbe.timeoutSeconds      | 30                       | Probe timeout for readiness probe                     |
| readinessProbe.failureThreshold    | 10                       | Failure threshold for readiness probe                 |
| readinessProbe.successThreshold    | 1                        | Success threshold for readiness probe                 |

### Pod Security Context Configuration

| Parameter                  | Default Value                 | Description                                           |
|----------------------------|-------------------------------|-------------------------------------------------------|
| podSecurityContext.fsGroup | 1000                          | fsGroup for ksqlDB Pod Security Context               |

### Container Security Context Configuration

| Parameter                                | Default Value     | Description                                           |
|------------------------------------------|-------------------|-------------------------------------------------------|
| securityContext.allowPrivilegeEscalation | false             | Allow privilege escalation for ksqlDB container       |
| securityContext.runAsUser                | 1000              | User ID for ksqlDB container                          |
| securityContext.runAsGroup               | 1000              | Group ID for ksqlDB container                         |
| securityContext.capabilities.drop        | ALL               | Drop Linux capabilities for ksqlDB container          |

### Container Resources Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| resources              | {}                               | Resource limits and requests for ksqlDB container     |

### NodeSelector, Tolerations, and Affinity Configuration

| Parameter              | Default Value                    | Description                                           |
|------------------------|----------------------------------|-------------------------------------------------------|
| nodeSelector           | {}                               | Node labels for pod assignment                        |
| tolerations            | {}                               | Tolerations for pod assignment                        |
| affinity               | {}                               | Affinity rules for pod assignment                     |

The above parameters map to the env variables defined in the [ksqlDB configuration](https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/server-config/) documentation. For more information please refer to the [ksqlDB documentation](https://docs.ksqldb.io/en/latest/operate-and-deploy/installation/server-config/).

## Enable basic authentication

Create a new file named `ksql-users.properties` with the following content:

```txt
admin: somepasstextplain,admin
dev: MD5:codeinmd5hash,developer
```

Create a new file named `ksql-jaas.conf` with the following content:

```txt
KsqlServer-Props {
  org.eclipse.jetty.jaas.spi.PropertyFileLoginModule required
  file="/etc/ksql/ksql-users.properties"
  debug="false";
};
```

Create a new secret with the files created above:

```bash
$ kubectl create secret generic ksql-users --from-file=ksql-users.properties -n kafka

$  kubectl create secret generic ksql-jaas --from-file=ksql-jaas.conf -n kafka
```

Enable basic authentication in the ksqlDB chart:

```bash
$ helm install --name my-release rdomenzain/ksqldb --set basicAuth.enabled=true --set basicAuth.existingSecretUsers=ksql-users --set basicAuth.existingSecretJaas=ksql-jaas
```

## Deploy ksqlDB in headless mode

Create a new file named `queries.sql` with the following content:

```sql
CREATE STREAM pageviews (viewtime BIGINT, userid VARCHAR, pageid VARCHAR) WITH (kafka_topic='pageviews', value_format='json');
```

Create a new ConfigMap with the file created above:

```bash
$ kubectl create configmap ksql-queries --from-file=queries.sql -n kafka
```

Enable headless mode in the ksqlDB chart:

```bash
$ helm install --name my-release rdomenzain/ksqldb --set queriesFileConfigMap=ksql-queries
```
