# Deployment

## TL;DR

```console
$ helm repo add xxx https://xxx/xxx
$ helm install my-release xxx/deployment
```
## Prerequisites

- Kubernetes 1.20
- Helm 3.7.1

## Installing the Chart
To install the chart with the release name `my-release`:

```console
$ helm install my-release xxx/deployment
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

## Parameters

### Common parameters

| Name                                    | Description                                                   | Value                         |
| --------------------------------------- | --------------------------------------------------------------| ----------------------------- |
| `image.repository`                      | Docker image repository                                       | `nginxinc/nginx-unprivileged` |
| `image.tag`                             | Docker image registry                                         | `stable-alpine`               |
| `image.pullPolicy`                      | Docker image pull policy                                      | `IfNotPresent`                |
| `imagePullSecrets`                      | Docker registry secret names as an array                      | `[]`                          |
| `replicaCount`                          | Number of desired replicates                                  | `1`                           |
| `env.<myenv>`                           | Add environment variable                                      | `""`                          |
| `configmap.<myconfigmap>`               | Create a ConfigMap and add it as an environment variable      | `"`                           |
| `secret.<mysecret>`                     | Create a Secret and add it as an environment variable         | `""`                          |
| `volume.<myvolume>`                     | Create an emptyDir volume and mount it                        | `""`                          |

### Network parameters

| Name                                    | Description                                                   | Value       |
| --------------------------------------- | --------------------------------------------------------------| ----------- |
| `ports.<myportname>.containerPort`      | Number of port to expose on the pod's IP address              | `8080`      |
| `ports.<myportname>.protocol`           | Protocol for port. Must be UDP, TCP, or SCTP                  | `TCP`       |
| `livenessProbe.<mycheck>.path`          | The check can be httpGet or tcpSocketDocker                   | `/`         |
| `livenessProbe.<mycheck>.port`          | Name or number of the port to access on the container         | `http`      |
| `readinessProbe.<mycheck>.path`         | The check can be httpGet or tcpSocketDocker                   | `/`         |
| `readinessProbe.<mycheck>.port`         | Name or number of the port to access on the container         | `http`      |
| `service.type`                          | What kind of Service (ClusterIP, NodePort or LoadBalancer)    | `ClusterIP` |
| `service.port`                          | Exposes the Service on port number                            | `80`        |

### ConfigmapFile parameters

| Name                                    | Description                                                   | Value    |
| --------------------------------------- | --------------------------------------------------------------| -------- |
| `configmapFile.<myconfigmap>.file`      | Create a ConfigMap from a file                                | `""`     |
| `configmapFile.<myconfigmap>.mountPath` | The path the volume will be mounted at                        | `"`      |
| `configmapFile.<myconfigmap>.subPath`   | The subdirectory of the volume to mount to                    | `""`     |
| `configmapFile.<myconfigmap>.readOnly`  | Set the volume as read-only                                   | `false`  |

### secretFile parameters

| Name                                    | Description                                                   | Value    |
| --------------------------------------- | --------------------------------------------------------------| -------- |
| `secretFile.<mysecret>.file`            | Create a Secret from a file                                   | `""`     |
| `secretFile.<mysecret>.mountPath`       | The path the volume will be mounted at                        | `"`      |
| `secretFile.<mysecret>.subPath`         | The subdirectory of the volume to mount to                    | `""`     |
| `secretFile.<mysecret>.readOnly`        | Set the volume as read-only                                   | `false`  |

## Examples

```console
$ helm install my-nginx . \
    --set env.env1=var1 \
    --set env.env2=var2 \
    --set configmap.map1=mapvar1 \
    --set configmap.map2=mapvar2 \
    --set secret.secret1=secretvar1 \
    --set secret.secret2=secretvar2 \
    --set configmapFile.mapfile1.file=configmapFile \
    --set configmapFile.mapfile1.mountPath=/tmp/map1 \
    --set configmapFile.mapfile1.subPath=map1 \
    --set secretFile.secretfile1.file=secretFile \
    --set secretFile.secretfile1.mountPath=/tmp/secret1 \
    --set secretFile.secretfile1.subPath=secret1 \
    --set secretFile.secretfile1.readOnly=true \
    --set volume.data=/data
```
