# Kafka Connect UI

This is a web tool for Kafka Connect for setting up and managing connectors for multiple connect clusters.

## Introduction

This chart bootstraps a [kafka-connect-ui](https://github.com/lensesio/kafka-connect-ui) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm repo add rdomenzain https://rdomenzain.github.io/helm-chart
$ helm install --name my-release rdomenzain/kafka-connect-ui
```

The command deploys Kafka Connect UI on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.


## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Kafka Connect UI chart and their default values.

| Parameter                        | Description                                                 | Default                  |
| -------------------------------  | ----------------------------------------------------------- | ------------------------ |
| replicaCount                     | desired number of controller pods                           | 1                        |
| image.repository                 | controller container image repository                       | landoop/kafka-connect-ui |
| image.tag                        | controller container image tag                              | 0.9.7                    |
| image.pullPolicy                 | controller container image pull policy                      | IfNotPresent             |
| nameOverride                     | String to override name template                            | ""                       |
| fullnameOverride                 | String to fully override fullname template                  | ""                       |
| service.type                     | ClusterIP, NodePort, or LoadBalancer                        | ClusterIP                |
| service.port                     | Service external port                                       | 80                       |
| ingress.enabled                  | Enable ingress controller resource                          | false                    |
| ingress.hosts                    | Ingress resource hostnames                                  | null                     |
| ingress.path                     | Ingress path                                                | /                        |
| ingress.annotations              | Ingress annotations configuration                           | {}                       |
| ingress.tls                      | Ingress TLS configuration                                   | null                     |
| resources                        | Server resource requests and limits                         | {}                       |
| nodeSelector                     | Node labels for pod assignment                              | {}                       |
| tolerations                      | Toleration labels for pod assignment                        | []                       |
| affinity                         | Affinity settings for pod assignment                        | {}                       |

The above parameters map to the env variables defined in [kafka-connect-ui](https://github.com/lensesio/kafka-connect-ui).
