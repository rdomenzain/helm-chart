# weblate

Weblate is a free web-based translation management system.

## TL;DR;

```console
$ helm repo add rdomenzain https://rdomenzain.github.io/helm-chart
$ helm install my-release rdomenzain/weblate
```

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | postgresql | 12.1.3 |
| https://charts.bitnami.com/bitnami | redis | 17.3.14 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| initContainers.enabled | bool | `false` |  |
| initContainers.volumeName | string | `weblate-customization` | Volume name |
| initContainers.containers | list | `[]` | Container script for initContainer |
| adminEmail | string | `""` | Email of Admin Account |
| adminPassword | string | `""` | Password of Admin Account |
| adminUser | string | `""` | Name of Admin Account |
| affinity | object | `{}` |  |
| allowedHosts | string | `"*"` | Hosts that are allowed to connect |
| caCertSecretName | string | `""` | Secret containing a custom CA cert bundle to be mounted. See https://docs.weblate.org/en/latest/admin/install.html?highlight=certificates#using-custom-certificate-authority |
| caCertSubPath | string | `""` | Name of the CA cert bundle in the secret, e.g. ca-certificates.crt or ca-bundle.crt |
| configOverride | string | `""` | Config override. See https://docs.weblate.org/en/latest/admin/install/docker.html#custom-configuration-files |
| containerSecurityContext.enabled | bool | `false` |  |
| debug | string | `"0"` | Enable debugging |
| defaultFromEmail | string | `""` | From email for outgoing emails |
| emailHost | string | `""` | Host for sending emails |
| emailPassword | string | `""` | Password for sending emails |
| emailPort | int | `587` | Port for sending emails |
| emailSSL | bool | `true` | Use SSL when sending emails |
| emailTLS | bool | `true` | Use TLS when sending emails |
| emailUser | string | `""` | User name for sending emails |
| existingSecret | string | `""` | Name of existing secret, Make sure it contains the keys postgresql-user, postgresql-password, redis-password, email-user, email-password, admin-user, admin-password Also note to set the existingSecret values for the Redis and Postgresql subcharts |
| externalSecretName | string | `""` | An external secret, in the same namespace, that will be use to set additionnal (environment) configs. |
| extraConfig | object | `{}` | Additional (environment) configs. Values will be evaluated as templates. See https://docs.weblate.org/en/latest/admin/install/docker.html#docker-environment |
| extraSecretConfig | object | `{}` | Same as `extraConfig`, but created as secrets. Values will be evaluated as Helm templates |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"weblate/weblate"` |  |
| image.tag | string | `"4.14.2-1"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"Prefix"` |  |
| ingress.ingressClassName | string | `""` |  |
| ingress.tls | list | `[]` |  |
| labels | object | `{}` | custom labels |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessMode | string | `"ReadWriteOnce"` |  |
| persistence.enabled | bool | `true` |  |
| persistence.existingClaim | string | `""` | Use an existing volume claim |
| persistence.filestore_dir | string | `"/app/data"` |  |
| persistence.size | string | `"10Gi"` |  |
| podSecurityContext.enabled | bool | `true` |  |
| podSecurityContext.fsGroup | int | `1000` |  |
| postgresql.auth.database | string | `"weblate"` |  |
| postgresql.auth.enablePostgresUser | bool | `true` |  |
| postgresql.auth.existingSecret | string | `""` |  |
| postgresql.auth.postgresPassword | string | `"weblate"` |  |
| postgresql.auth.secretKeys.userPasswordKey | string | `"postgresql-password"` |  |
| postgresql.enabled | bool | `true` |  |
| postgresql.postgresqlHost | string | `None` | External postgres database endpoint, to be used if `postgresql.enabled == false` |
| postgresql.service.ports.postgresql | int | `5432` |  |
| redis.architecture | string | `"standalone"` |  |
| redis.auth.enabled | bool | `true` |  |
| redis.auth.existingSecret | string | `""` |  |
| redis.auth.existingSecretPasswordKey | string | `"redis-password"` |  |
| redis.auth.password | string | `"weblate"` |  |
| redis.db | int | `1` |  |
| redis.enabled | bool | `true` |  |
| redis.redisHost | string | `None` | External redis database endpoint, to be used if `redis.enabled == false` |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| serverEmail | string | `""` | Sender for outgoing emails |
| service.annotations | string | `nil` |  |
| service.port | int | `80` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| siteDomain | string | `"chart-example.local"` | Site domain |
| siteTitle | string | `"Weblate"` |  |
| tolerations | list | `[]` |  |
| updateStrategy | string | `"Recreate"` |  |

## Configure the `initContainer` section

This configuration will allow you to perform actions before building the main container, it is useful if you need to customize weblate. A typical configuration is to download the new weblate configuration file (logos, favicon, etc) and unzip.

For more information see: [Customizing Weblate](https://docs.weblate.org/en/latest/admin/customize.html)

```yaml
initContainers:
  enabled: true
  volumeName: weblate-customization
  containers: 
    - name: init-script-downloader
      image: appropriate/curl
      args:
        - "-o"
        - "/tmp/data/weblate_customization.zip"
        - "https://file.example.com"
      volumeMounts:
      - mountPath: /tmp/data
        name: weblate-customization
    - name: init-script-unzip
      image: alpine:3.12
      command: ["sh", "-c", "unzip /tmp/data/weblate_customization.zip -d /tmp/data/"]
      volumeMounts:
      - mountPath: /tmp/data
        name: weblate-customization
```
