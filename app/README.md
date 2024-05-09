# app

Universal Helm chart for application. Uses [semantic versioning](https://semver.org/) for safe updates and compatibility. Documentation generated with [helm-docs](https://github.com/norwoodj/helm-docs)

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| himaster | <vitalibicov83@gmail.com> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| additionalExternalConfigVolumes | list | `[]` | There are several options to define volumes via the external secret. |
| additionalExternalSecretVolumes | list | `[]` |  |
| additionalNfsPvc | list | `[]` | Add PVC mounted from NFS |
| additionalPvc | list | `[]` | Add additional shared volume (mounts directory from node) |
| additionalRamPvc | list | `[]` | Add PVC in RAM (very fast) |
| additionalSecretVolumes | list | `[]` | Adds secret from data and mounts it in mountPath |
| affinity | bool | `true` | Add [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) fow web application's Deployment |
| affinity_required | bool | `true` |  |
| appCommand | object | `{"args":"","command":"","enabled":false}` | Defines [Lifecycle poststart hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for app container   command:   - ... |
| appCommand.args | string | `""` | Defines custom args for "app" container |
| appCommand.command | string | `""` | Defines custom command for "app" container |
| appCommand.enabled | bool | `false` | Enables custom command and args for "app" container |
| appDocRoot | string | `"/var/www/html"` | Defines Web  application docroot. Creates shared volume for "app" and "nginx" containers. Populated with data by "data" initContainer. |
| appLivenessProbe.command | string | `"- php-fpm-healthcheck\n"` | Defines command of exec liveness probe |
| appLivenessProbe.enabled | bool | `true` | Enables [liveness probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-command) for app container |
| appLivenessProbe.failureThreshold | string | `""` | Defines failureThreshold of liveness probe |
| appLivenessProbe.httpHeaders | list | `[]` | Defines httpHeaders of httpGet liveness probe |
| appLivenessProbe.httpPath | string | `"/"` | Defines path of httpGet liveness probe |
| appLivenessProbe.httpPort | int | `80` | Defines port of httpGet liveness probe |
| appLivenessProbe.httpScheme | string | `"HTTP"` | Defines scheme of httpGet liveness probe |
| appLivenessProbe.initialDelaySeconds | int | `0` | Defines initialDelaySeconds of liveness probe |
| appLivenessProbe.periodSeconds | int | `10` | Defines periodSeconds of liveness probe |
| appLivenessProbe.successThreshold | string | `""` | Defines successThreshold of liveness probe |
| appLivenessProbe.tcpSocketPort | int | `9000` | Defines port of tcpSocket liveness probe |
| appLivenessProbe.timeoutSeconds | string | `""` | Defines timeoutSeconds of liveness probe |
| appLivenessProbe.type | string | `"command"` | Defines liveness probe type. Possible values: "command", "socket" and "httpGet" |
| appPort.name | string | `"node"` | Defines port name of "app" container |
| appPort.number | int | `3000` | Defines port number of "app" container |
| appReadinessProbe.command | string | `"- php-fpm-healthcheck\n"` | Defines command of exec readiness probe |
| appReadinessProbe.enabled | bool | `true` | Enables [readiness probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes) for app container |
| appReadinessProbe.failureThreshold | string | `""` | Defines failureThreshold of readiness probe |
| appReadinessProbe.httpHeaders | list | `[]` | Defines httpHeaders of httpGet readiness probe |
| appReadinessProbe.httpPath | string | `"/"` | Defines path of httpGet readiness probe |
| appReadinessProbe.httpPort | int | `80` | Defines port of httpGet readiness probe |
| appReadinessProbe.httpScheme | string | `"HTTP"` | Defines scheme of httpGet readiness probe |
| appReadinessProbe.initialDelaySeconds | int | `1` | Defines initialDelaySeconds of readiness probe |
| appReadinessProbe.periodSeconds | int | `5` | Defines periodSeconds of readiness probe |
| appReadinessProbe.successThreshold | string | `""` | Defines successThreshold of readiness probe |
| appReadinessProbe.tcpSocketPort | int | `9000` | Defines port of tcpSocket readiness probe |
| appReadinessProbe.timeoutSeconds | string | `""` | Defines timeoutSeconds of readiness probe |
| appReadinessProbe.type | string | `"command"` | Defines readiness probe type. Possible values: "command", "socket" and "httpGet" |
| budget | object | `{"maxUnavailable":"20%"}` | Enables [PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) creation |
| budget.maxUnavailable | string | `"20%"` | Configures disruption budget limits minAvailable: |
| clusterName | string | `"test"` | Used in spec.update.path of [ImageUpdateAutomation](https://fluxcd.io/flux/components/image/imageupdateautomations/) |
| commonLabels.cluster | string | `"Unknown"` |  |
| commonLabels.develop_team | string | `"Unknown"` |  |
| commonLabels.env | string | `"Unknown"` |  |
| commonLabels.owner | string | `"Unknown"` |  |
| commonLabels.type | string | `"Unknown"` |  |
| customLabels | object | `{}` |  |
| data.customCommands | list | `[]` | set custom commands which you want to run in "data" initContainer in web application |
| data.resources | object | `{}` | configures resources (requests/limits) for "data" initContainer in web application |
| data.sharedNfsPvc | bool | `false` | add a shared app nfs pvc in "data" initContainer in web application |
| deployment.enabled | bool | `true` | Enables main Deployment creation. Needed for web service. |
| env | list | `[]` | Environment variable in "app" container |
| extraAppPorts | list | `[]` |  |
| extraContainers | list | `[]` |  |
| extraInitContainers | list | `[]` |  |
| extraVolumes | list | `[]` |  |
| fluxv2 | bool | `true` | Enable compatibility with Flux system (https://fluxcd.io/flux/concepts/) |
| fullnameOverride | string | `""` | is the string to fully override the fullname template. |
| hostAliases | object | `{}` | Adding entries to Pod /etc/hosts with [HostAliases](https://kubernetes.io/docs/tasks/network/customize-hosts-file-for-pods/) |
| hpa | object | `{"apiVersion":"autoscaling/v1","maxReplicas":10,"metrics":{"enabled":false,"rules":[]},"minReplicas":2,"targetCPUUtilizationPercentage":70}` | Enable [HorisontalPodAutoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) |
| hpa.apiVersion | string | `"autoscaling/v1"` | HorisontalPodAutoscaler API version |
| hpa.maxReplicas | int | `10` | Maximum auto scaling limit |
| hpa.metrics.enabled | bool | `false` | [Custom and external metrics](https://cloud.google.com/kubernetes-engine/docs/concepts/custom-and-external-metrics) for autoscaling workloads |
| hpa.metrics.rules | list | `[]` | If you need to scale your workload based on the performance of an application or service outside of Kubernetes, you can configure an external metric |
| hpa.minReplicas | int | `2` | Minimum auto scaling limit |
| hpa.targetCPUUtilizationPercentage | int | `70` | Target CPU utilization percentage. [Algorithm details](https://github.com/kubernetes/website/blob/main/content/en/docs/tasks/run-application/horizontal-pod-autoscale.md#algorithm-details) |
| image.automationSuspend | string | `"false"` |  |
| image.defaultPolicy.semver.range | string | `">=1.0.0"` |  |
| image.imagePullSecrets | list | `[]` | Define the list of imagePullSecrets for main deployment/statefullset, cronjobs and workers, default secret won't be overwritten. |
| image.image_ver_updater_enabled | bool | `true` | Enable image version auto-update resources (fluxv2 must be "true") |
| image.pullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of main image. Possible values: "IfNotPresent", "Always" or "Never" |
| image.repoSecretName | string | `"imagesecret"` | Secret for [ImageRepository](https://fluxcd.io/flux/components/image/imagerepositories/) in Flux v2. |
| image.repository | string | `"laravel:latest"` | main image name and version. Used in data and app containers of web application, in app container of worker and in cron container of cronjob. |
| ingress.annotations | object | `{"kubernetes.io/ingress.class":"nginx","kubernetes.io/tls-acme":"true","nginx.ingress.kubernetes.io/configuration-snippet":"proxy_set_header Authorization $http_authorization;\nproxy_pass_header Authorization;\n","nginx.ingress.kubernetes.io/proxy-read-timeout":"14400","nginx.ingress.kubernetes.io/ssl-redirect":"true","prometheus.io/port":"10254","prometheus.io/scrape":"true"}` | Ingres's [spec.metadata.annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| ingress.basicAuth.auth | string | `""` | Creates /opt/.htpasswd file |
| ingress.basicAuth.custom | bool | `false` | Removes /opt/.htpasswd file when enabled |
| ingress.basicAuth.enabled | bool | `false` | Add Basic Auth functionality to ingresses |
| ingress.enabled | bool | `true` | Enable [Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/) creation |
| ingress.ingressClassName | string | `"nginx"` | Nginx is configured to automatically discover all ingress with the kubernetes.io/ingress.class: "nginx" annotation or where ingressClassName: nginx is present |
| ingress.skins | list | `[]` | Array of groups of domains |
| nameOverride | string | `""` | is the string to partially override fullname template (will maintain the release name) and fully override name template. |
| nginx.additionalPvc | list | `[]` | Add additional shared volume (mounts directory from node) |
| nginx.config | string | `"server {\n  listen 80  default_server;\n  index      index.php index.html;\n  error_log  /dev/stderr warn;\n  access_log /dev/null;\n  root       /var/www/html/public;\n  location / {\n      try_files       $uri $uri/ /index.php?$query_string;\n  }\n  location = /favicon.ico {\n    try_files               $uri $uri/ /favicon.php;\n  }\n  location ~* \\.php$ {\n      try_files               $uri = 404;\n      fastcgi_pass            127.0.0.1:9000;\n      include                 fastcgi_params;\n      fastcgi_param           SCRIPT_FILENAME $document_root$fastcgi_script_name;\n      fastcgi_param           PATH_INFO $fastcgi_path_info;\n      fastcgi_param           HTTPS $http_x_forwarded_proto if_not_empty;\n      fastcgi_param           SERVER_PORT $http_x_forwarded_port;\n      fastcgi_param           HTTP_X_REQUEST_START \"t=${msec}\";\n      fastcgi_param           REMOTE_ADDR $http_x_real_ip;\n      fastcgi_hide_header     X-Powered-By;\n      fastcgi_read_timeout    6000;\n  }\n  location ~* \\.(jpg|jpeg|gif|png|bmp|swf|css|js|cur|(gz&!xml.gz)|pdf|img|ttf|woff|woff2|svg|lic)$ {\n      access_log              off;\n      expires                 360d;\n      add_header              Cache-Control public;\n  }\n  location /status {\n      stub_status;\n      auth_basic off;\n      allow all;\n  }\n  location ~ /\\. {\n      deny                    all;\n  }\n}\n"` | Nginx config file /etc/nginx/conf.d/default.conf |
| nginx.customConfig | object | `{"client_body_timeout":10,"keepalive_timeout":0,"worker_connections":4096}` | Nginx config file /etc/nginx/nginx.conf |
| nginx.customConfig.client_body_timeout | int | `10` | Defines a timeout for reading client request body. (https://nginx.org/en/docs/http/ngx_http_core_module.html#client_body_timeout) |
| nginx.enabled | bool | `false` | Enables adding of [Nginx](https://nginx.org/en/) sidecar container |
| nginx.image | string | `"nginx:1.17"` | nginx image name and version. Used in "nginx" container of web application. |
| nginx.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of nginx image. Possible values: "IfNotPresent", "Always" or "Never" |
| nginx.livenessProbe.command | string | `nil` | Defines command of exec liveness probe |
| nginx.livenessProbe.enabled | bool | `true` | Enables httpGet [liveness probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-command) for nginx container |
| nginx.livenessProbe.failureThreshold | int | `3` | Defines failureThreshold of liveness probe  |
| nginx.livenessProbe.httpHeaders | list | `[]` | Defines httpHeaders of httpGet liveness probe |
| nginx.livenessProbe.httpPath | string | `"/status"` | Defines path of httpGet liveness probe |
| nginx.livenessProbe.httpPort | int | `80` | Defines port of httpGet liveness probe  |
| nginx.livenessProbe.httpScheme | string | `""` | Defines scheme of httpGet liveness probe |
| nginx.livenessProbe.initialDelaySeconds | int | `10` | Defines initialDelaySeconds of liveness probe  |
| nginx.livenessProbe.periodSeconds | int | `3` | Defines periodSeconds of liveness probe  |
| nginx.livenessProbe.successThreshold | string | `""` | Defines successThreshold of liveness probe |
| nginx.livenessProbe.tcpSocketPort | string | `nil` | Defines port of tcpSocket liveness probe |
| nginx.livenessProbe.timeoutSeconds | int | `5` | Defines timeoutSeconds of liveness probe  |
| nginx.livenessProbe.type | string | `"httpGet"` | Defines liveness probe type. Possible values: "command", "socket" and "httpGet" default value "httpGet" |
| nginx.prepopulate | bool | `false` | If enabled uses shared volume for docroot |
| nginx.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10; /usr/sbin/nginx -s quit"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for nginx container |
| nginx.readinessProbe.enabled | bool | `true` | Enables httpGet [readiness probe](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes) for nginx container |
| nginx.readinessProbe.failureThreshold | int | `3` | Defines failureThreshold of readiness probe |
| nginx.readinessProbe.host | string | `""` | Defines host of httpGet readiness probe |
| nginx.readinessProbe.path | string | `"/"` | Defines path of httpGet readiness probe |
| nginx.readinessProbe.periodSeconds | int | `10` | Defines periodSeconds of readiness probe |
| nginx.readinessProbe.successThreshold | int | `1` | Defines successThreshold of readiness probe |
| nginx.readinessProbe.timeoutSeconds | int | `5` | Defines timeoutSeconds of readiness probe |
| nginx.resources.limits.memory | string | `"1Gi"` | configures limits of RAM for "nginx" container |
| nginx.resources.requests.cpu | string | `"500m"` | configures requests of CPU for "nginx" container |
| nginx.resources.requests.memory | string | `"1Gi"` | configures requests of RAM for "nginx" container |
| nginx.sharedNfsPvc | bool | `false` | add a shared app nfs pvc in a "nginx" container |
| nodeSelector | object | `{}` | [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) fow web application's Deployment |
| podName | object | `{"enabled":false}` | to enable POD_NAME env variable |
| prestop.command | list | `["/bin/bash","-c","/bin/sleep 10; kill -QUIT 1"]` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for app container |
| ramDocroot.enabled | bool | `false` | Creates shared volume in RAM for "app" and "nginx" containers |
| ramDocroot.size | string | `"2Gi"` | Defines RAM shared volume size |
| rbac.annotations | object | `{}` | Custom ServiceAccount annotations |
| rbac.apiGroups | list | `[""]` | Specifies allowed apiGroups for Role/ClusterRole |
| rbac.enabled | bool | `false` | Enables [RBAC](https://cloud.google.com/kubernetes-engine/docs/how-to/role-based-access-control) for application. |
| rbac.existingRoleName | string | `""` | Allows existing Role/ClusterRole usage |
| rbac.level | string | `"namespace"` | Specifies the Role or ClusterRole object to be created. Possible values: namespace - Role object to be created. cluster - ClusterRole object to be created. |
| rbac.resources | list | `["*"]` | Specifies allowed resources for Role/ClusterRole |
| rbac.verbs | list | `["get","list"]` | Specifies allowed verbs for Role/ClusterRole |
| replicas | int | `1` | Default replicas number |
| secret_env | object | `{"envs":[],"secretRef":"","secretRefNames":[]}` | Environment variable from an existing secret in "app" container |
| secret_env.envs | list | `[]` | array of variables names and secret's keys |
| secret_env.secretRef | string | `""` | existing secret name |
| secret_env.secretRefNames | list | `[]` | Please use secretRefNames for set existing secret's names |
| service.enabled | bool | `true` | Enables Kubernetes [Service object](https://kubernetes.io/docs/concepts/services-networking/service/) creation |
| service.extraServicePorts | list | `[]` | extra port for service |
| service.loadBalancerSourceRanges | list | `["127.0.0.1/32","10.0.0.0/8"]` | In order to limit which client IP's can access the Network Load Balancer, specify loadBalancerSourceRanges. NOT WORKS WITH FLANNEL |
| service.name | string | `"http-web"` | Name of port in service |
| service.port | int | `80` | Defines Service port number |
| service.protocol | string | `"TCP"` | Defines Service port's protocol |
| service.targetName | string | `"http"` | Name of port in pod |
| service.type | string | `"NodePort"` | Defines Service type Possible values: "NodePort", "ClusterIP", "LoadBalancer" or "ExternalName" |
| serviceAccountName | string | `""` | Set the service account name for the release. |
| serviceMonitor.enabled | bool | `false` | If true, a ServiceMonitor CRD is created for a prometheus operator https://github.com/coreos/prometheus-operator |
| serviceMonitor.endpoints | list | `[{"honorLabels":true,"interval":"10s","metricRelabelings":[],"path":"/metrics","port":"http-metrics","relabelings":[{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_pod_label_app"],"targetLabel":"app"},{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_namespace"],"targetLabel":"branch"}],"scheme":"http","scrapeTimeout":"10s"}]` | ServiceMonitor endpoint path |
| serviceMonitor.endpoints[0] | object | `{"honorLabels":true,"interval":"10s","metricRelabelings":[],"path":"/metrics","port":"http-metrics","relabelings":[{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_pod_label_app"],"targetLabel":"app"},{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_namespace"],"targetLabel":"branch"}],"scheme":"http","scrapeTimeout":"10s"}` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).relabelings param of ServiceMonitor object. [Relabelings vs metricRelabelings](https://github.com/prometheus-operator/prometheus-operator/issues/3246) |
| serviceMonitor.externalExporter | bool | `true` | Enable "monitoring" sidecar container |
| serviceMonitor.image | string | `"hipages/php-fpm_exporter:2.2"` | [php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) image name and version. Used in "monitoring" sidecar container of application. |
| serviceMonitor.interval | string | `"10s"` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).interval param of ServiceMonitor object |
| serviceMonitor.labels | object | `{}` | Labels added to ServiceMonitor object |
| serviceMonitor.metricRelabelings | list | `[]` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).metricRelabelings param of ServiceMonitor object. [Relabelings vs metricRelabelings](https://github.com/prometheus-operator/prometheus-operator/issues/3246) |
| serviceMonitor.metricsPort | int | `9253` | Monitoring Port to be exported by Service |
| serviceMonitor.relabelings | list | `[{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_pod_label_app"],"targetLabel":"app"},{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_namespace"],"targetLabel":"branch"}]` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).relabelings param of ServiceMonitor object. [Relabelings vs metricRelabelings](https://github.com/prometheus-operator/prometheus-operator/issues/3246) |
| serviceMonitor.resources.limits.memory | string | `"50Mi"` | configures limits of RAM for "monitoring" container in web application |
| serviceMonitor.resources.requests.cpu | string | `"50m"` | configures requests of CPU for "monitoring" container in web application |
| serviceMonitor.resources.requests.memory | string | `"50Mi"` | configures requests of RAM for "monitoring" container in web application |
| serviceMonitor.scheme | string | `"http"` | endpoints.scheme param of ServiceMonitor object |
| serviceMonitor.scrapeTimeout | string | `"10s"` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).scrapeTimeout param of ServiceMonitor object |
| statefulset.accessModes | list | `["ReadWriteOnce"]` | PVC Access Modes for volume |
| statefulset.enabled | bool | `false` | Enables Statefulset creation. |
| statefulset.extraVolumeClaimTemplates | list | `[]` |  |
| statefulset.podManagementPolicy | string | `""` | podManagementPolicy to manage scaling operation of pods (only in StatefulSet mode) |
| statefulset.size | string | `"8Gi"` | PVC Storage Request for volume |
| statefulset.storageClass | string | `""` | PVC Storage Class for volume |
| statefulset.updateStrategy | object | `{"type":"RollingUpdate"}` | can be set to RollingUpdate or OnDelete |
| terminationGracePeriodSeconds | int | `30` | Configures [Hook handler execution](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#hook-handler-execution) |
| tolerations | list | `[]` | Add [toleration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) fow web application's Deployment |