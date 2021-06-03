# service-restarter

This chart is used for restarting Kubernetes workloads like deployments, daemonsets and statefulsets via `kubectl rollout restart`. Sometimes this is the easy way to keep things running.

| Value | Description | Default |
|-------|-------------|---------|
| successfulJobsHistoryLimit | The `successfulJobsHistoryLimit` for every CronJob. | 1 |
| failedJobsHistoryLimit | The `failedJobsHistoryLimit` for every CronJob. | 1 |
| image.repository | The kubectl image. | "public.ecr.aws/bitnami/kubectl" |
| image.pullPolicy | Image pull polocy. | "IfNotPresent" |
| image.tag | Image tag. | `""` <br> When this value is left blank, it will use Kubernetes cluster verison as `"<Major>.<Minor>"`, like `"1.21"`. |
| imagePullSecrets | Image pull secrets. | `[]` |
| nameOverride | Name override for this helm chart. | `""` |
| fullnameOverride | Name override for this helm chart. | `""` |
| resources.limits.cpu | CPU limit. | `"50m"` |
| resources.limits.memory | Memory limit. | `"64Mi"` |
| resources.requests.cpu | CPU request. | `"50m"` |
| resources.requests.cpu | Memory request. | `"64Mi"` |
| nodeSelector | `nodeSelector` of Pod. | `{}` |
| tolerations | `tolerations` of Pod. | `[]` |
| affinity | `affinity` of Pod. | `{}` |
| restartPolicy | `restartPolicy` of Pod. | `{}` |
| targetServices | Array of services to restart. Properties: <ul><li>`namespace`: `<string>`</li><li>`kind`: `deployment \| daemonset \| statefulset`</li><li>`name`: `<string>`</li><li>`schedule`: `"* * * * *"`</li></ul> | `[]` |

## Example

```bash
$ helm repo add wtchangdm https://wtchangdm.github.io/helm-charts

$ helm upgrade --install service-restarter wtchangdm/service-restarter \
                --namespace some-ns --create-namespace \
                --set "targetServices[0].namespace=ns-1" \
                --set "targetServices[0].kind=deployment" \
                --set "targetServices[0].name=nginx" \
                --set "targetServices[0].schedule=* * * * *"
```
