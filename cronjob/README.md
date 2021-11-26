# CronJob

## TL;DR

```console
$ helm repo add xxx https://xxx/xxx
$ helm install my-release xxx/cronjob
```
## Prerequisites

- Kubernetes 1.20
- Helm 3.7.1

## Installing the Chart
To install the chart with the release name `my-release`:

```console
$ helm install my-release xxx/cronjob
```

## Uninstalling the Chart

To uninstall/delete the `my-release` cronjob:

```console
$ helm delete my-release
```

## Parameters

### Common parameters

| Name                                    | Description                                                   | Value               |
| --------------------------------------- | --------------------------------------------------------------| ------------------- |
| `image.repository`                      | Docker image repository                                       | `docker.io/busybox` |
| `image.tag`                             | Docker image registry                                         | `stable`            |
| `image.pullPolicy`                      | Docker image pull policy                                      | `IfNotPresent`      |
| `image.command`                         | Docker image command                                          | `["echo"]`          |
| `image.args`                            | Docker image args                                             | `["cronjob"]`       |
| `imagePullSecrets`                      | Docker registry secret names as an array                      | `[]`                |
| `schedule`                              | CronJob schedule expressions, you can also use crontab.guru.  | `"*/1 * * * *"`     |
| `restartPolicy`                         | Possible values Always, OnFailure and Never                   | `OnFailure`         |
| `concurrencyPolicy`                     | How to treat concurrent executions of a job that is created   | `Allow`             |
| `suspend`                               | If it is set to true, all subsequent executions are suspended | `false`             |
| `successfulJobsHistoryLimit`            | How many completed jobs should be kept                        | `3`                 |
| `failedJobsHistoryLimit`                | How many failed jobs should be kept                           | `1`                 |
| `startingDeadlineSeconds`               | Deadline in seconds for starting the job                      | `200`               |
| `env.<myenv>`                           | Add environment variable                                      | `""`                |
| `configmap.<myconfigmap>`               | Create a ConfigMap and add it as an environment variable      | `"`                 |
| `secret.<mysecret>`                     | Create a Secret and add it as an environment variable         | `""`                |
| `volume.<myvolume>`                     | Create an emptyDir volume and mount it                        | `""`                |

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
$ helm install my-cronjob . \
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