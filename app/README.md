# app

Universal Helm chart for PHP application. Uses [semantic versioning](https://semver.org/) for safe updates and compatibility. Documentation generated with [helm-docs](https://github.com/norwoodj/helm-docs)

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| v.bicov | <himaster@autodoc.eu> |  |
| v.krailo | <v.krailo@autodoc.eu> |  |
| a.chelak | <a.chelak@autodoc.eu> |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| accountName | string | `"autodoc-234411"` | Used for setting GOOGLE_CLOUD_PROJECT environment variables in many containers. |
| additionalExternalConfigVolumes | list | `[]` | There are several options to define volumes via the external secret. |
| additionalExternalSecretVolumes | list | `[]` |  |
| additionalNfsPvc | list | `[]` | Add PVC mounted from NFS |
| additionalPvc | list | `[]` | Add additional shared volume (mounts directory from node) |
| additionalRamPvc | list | `[]` | Add PVC in RAM (very fast) |
| additionalSecretVolumes | list | `[]` | Adds secret from data and mounts it in mountPath |
| affinity | bool | `true` | Add [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) fow web application's Deployment |
| affinity_required | bool | `true` |  |
| annotator.customEnvs | list | `[]` | Add custom Environment variables to post-install,post-upgrade Helm hook from secret. |
| annotator.enabled | bool | `true` | Enables annotator functionality. Creates 3 Helm hooks pre-install,pre-upgrade - integration with GitLab, changes stage status in pipeline to "in progress". post-install,post-upgrade - integration with GitLab, changes stage status in pipeline to "success", integration with NewRelic and Grafana - adds deployment mark. post-rollback - integration with GitLab, changes stage status in pipeline to "failed". |
| annotator.imagePullSecrets | list | `[]` | Define the list of imagePullSecrets for annotator's jobs, default secret won't be overwritten. |
| annotator.postfix | string | `""` | Used for GitLab integration. Stage name for integration creates by pattern "deploy{{ .Values.annotator.postfix }}" |
| annotator.pullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of annotator image. Possible values: "IfNotPresent", "Always" or "Never" |
| annotator.resources.limits.memory | string | `"256Mi"` | configures limits of RAM for annotator pod |
| annotator.resources.requests.cpu | string | `"100m"` | configures requests of CPU for annotator pod |
| annotator.resources.requests.memory | string | `"256Mi"` | configures requests of RAM for annotator pod |
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
| appPort.name | string | `"tcp-fpm"` | Defines port name of "app" container |
| appPort.number | int | `9000` | Defines port number of "app" container |
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
| application | object | `{"enabled":false}` | Defines custom application config (DEPRECATED) appConfig: |   test config |
| application.enabled | bool | `false` | Enabling support of [Kubernetes Applications](https://github.com/kubernetes-sigs/application) |
| budget | object | `{"maxUnavailable":"20%"}` | Enables [PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) creation |
| budget.maxUnavailable | string | `"20%"` | Configures disruption budget limits minAvailable: |
| builtInManagedSecrets | list | `[]` | Enable the list of built-in managedSecret objects. |
| chproxy.config | string | `"# by default each cluster has `default` user which can be overridden by section `users`\n"` | Set content of chproxy.yml file |
| chproxy.debug | bool | `false` | Set log_debug param of chproxy |
| chproxy.enabled | bool | `false` | Enables [Chproxy](https://www.chproxy.org/) sidecar container |
| chproxy.image | string | `"eu.gcr.io/autodoc-234411/chproxy:latest"` | chproxy image name and version. Used in "chproxy" sidecar container of application. |
| chproxy.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of chproxy image. Possible values: "IfNotPresent", "Always" or "Never" |
| chproxy.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for chproxy container |
| chproxy.resources.limits.memory | string | `"200Mi"` | configures limits of RAM for "chproxy" container |
| chproxy.resources.requests.cpu | string | `"100m"` | configures requests of CPU for "chproxy" container |
| chproxy.resources.requests.memory | string | `"200Mi"` | configures requests of RAM for "chproxy" container |
| cliAffinity | bool | `false` | Add [affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity) for additional workloads (crons etc.) |
| cliNodeSelector | object | `{}` | [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) for additional workloads (crons etc.) |
| cliTolerations | list | `[]` | Add [toleration](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for additional workloads (crons etc.) |
| clusterName | string | `"shop-gclus-prod"` | Used in spec.update.path of [ImageUpdateAutomation](https://fluxcd.io/flux/components/image/imageupdateautomations/) |
| commonLabels.cluster | string | `"Unknown"` |  |
| commonLabels.develop_team | string | `"Unknown"` |  |
| commonLabels.devops_team | string | `"Unknown"` |  |
| commonLabels.env | string | `"Unknown"` |  |
| commonLabels.owner | string | `"Unknown"` |  |
| commonLabels.type | string | `"Unknown"` |  |
| commonLabels.vs | string | `"Unknown"` |  |
| commonLabels.vsc | string | `"Unknown"` |  |
| cronJobs | list | `[]` | Array of [CronJobs](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) cronJobsPreStop: # -- Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for cronjob containers   command:      - ls      - -al      - /bin/     - ... cronJobsPostStart: # -- Defines [Lifecycle proststart hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for cronjob containers   command:      - ls      - -al      - /bin/     - .... |
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
| fluxv2 | bool | `false` | Enable compatibility with Flux system (https://fluxcd.io/flux/concepts/) |
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
| image.imagePullSecrets | list | `[]` | Define the list of imagePullSecrets for main deployment/statefullset, cronjobs and workers, default secret won't be overwritten. |
| image.pullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of main image. Possible values: "IfNotPresent", "Always" or "Never" |
| image.repoSecretName | string | `"imagesecret"` | Secret for [ImageRepository](https://fluxcd.io/flux/components/image/imagerepositories/) in Flux v2. |
| image.repository | string | `"laravel:latest"` | PHP main image name and version. Used in data and app containers of web application, in app container of worker and in cron container of cronjob. |
| ingress.annotations | object | `{"kubernetes.io/ingress.class":"nginx","kubernetes.io/tls-acme":"true","nginx.ingress.kubernetes.io/configuration-snippet":"proxy_set_header Authorization $http_authorization;\nproxy_pass_header Authorization;\n","nginx.ingress.kubernetes.io/proxy-read-timeout":"14400","nginx.ingress.kubernetes.io/ssl-redirect":"true","prometheus.io/port":"10254","prometheus.io/scrape":"true"}` | Ingres's [spec.metadata.annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| ingress.basicAuth.auth | string | `"user:$apr1$48RnMqYu$TosK2FaS06.VW1RJxp6/c/\ntest:$apr1$vmrA9a.b$Q5ugr6hnV62x/82rnN3FT0\n"` | Creates /opt/.htpasswd file |
| ingress.basicAuth.custom | bool | `false` | Removes /opt/.htpasswd file when enabled |
| ingress.basicAuth.enabled | bool | `false` | Add Basic Auth functionality to ingresses |
| ingress.enabled | bool | `true` | Enable [Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/) creation |
| ingress.skins | list | `[]` | Array of groups of domains |
| ingressInternal.annotations | object | `{"kubernetes.io/ingress.class":"nginx-internal"}` | Ingres's [spec.metadata.annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) |
| ingressInternal.defaultHost | object | `{"enabled":true}` | Default internal domain |
| ingressInternal.enabled | bool | `false` | Enable [Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/) creation |
| ingressInternal.hosts | list | `[]` | Array of internal domains |
| istio.authorizationPolicyRules | list | `[{}]` | [AuthorizationPolicy](https://istio.io/latest/docs/reference/config/security/authorization-policy/) rules. |
| istio.enabled | bool | `false` | Adds Istio Service Mesh annotation to Deployment and [AuthorizationPolicy](https://istio.io/latest/docs/reference/config/security/authorization-policy/) object. |
| istio.revision | string | `"asm-1106-2"` | Specifies version if installed Istio. |
| migration.command | string | `"php artisan migrate --force"` | Configures migration command |
| migration.enabled | bool | `false` | Enable post-install,post-upgrade Helm hook for database migration |
| mongobetween.config | string | `"/tmp/mongo.sock=mongodb://127.0.0.1:27017"` | Config for mongobetween app |
| mongobetween.enabled | bool | `false` | Enables [mongobetween](https://github.com/coinbase/mongobetween) sidecar container |
| mongobetween.image | string | `"europe-docker.pkg.dev/autodoc-234411/helpers/mongobetween:0.0.9"` | mongobetween image name and version. Used in "mongobetween" sidecar container of application. |
| mongobetween.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of mongobetween image. Possible values: "IfNotPresent", "Always" or "Never" |
| mongobetween.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for mongobetween container |
| mongobetween.resources.limits.memory | string | `"300Mi"` | configures limits of RAM for "mongobetween" container in web application |
| mongobetween.resources.requests.cpu | string | `"300m"` | configures requests of CPU for "mongobetween" container in web application |
| mongobetween.resources.requests.memory | string | `"300Mi"` | configures requests of RAM for "mongobetween" container in web application |
| mongos.configdb | string | `"autodoc-configsvr/configsvr-mongodb-replicaset-0.configsvr-mongodb-replicaset.mongodb.svc.cluster.local:27017,configsvr-mongodb-replicaset-1.configsvr-mongodb-replicaset.mongodb.svc.cluster.local:27017,configsvr-mongodb-replicaset-2.configsvr-mongodb-replicaset.mongodb.svc.cluster.local:27017"` | Config string of mongo router |
| mongos.cronResources.limits.memory | string | `"300Mi"` | configures limits of RAM for "mongos" container in cron jobs/workers |
| mongos.cronResources.requests.cpu | string | `"100m"` | configures requests of CPU for "mongos" container in cron jobs/workers |
| mongos.cronResources.requests.memory | string | `"300Mi"` | configures requests of RAM for "mongos" container in cron jobs/workers |
| mongos.enabled | bool | `false` | Enables [mongos](https://www.mongodb.com/docs/manual/core/sharded-cluster-query-router/) sidecar container |
| mongos.image | string | `"eu.gcr.io/autodoc-234411/mongos:4.0.7"` | mongos image name and version. Used in "mongos" sidecar container of application. |
| mongos.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of mongos image. Possible values: "IfNotPresent", "Always" or "Never" |
| mongos.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for mongos container |
| mongos.resources.limits.memory | string | `"500Mi"` | configures limits of RAM for "mongos" container in web application |
| mongos.resources.requests.cpu | string | `"1"` | configures requests of CPU for "mongos" container in web application |
| mongos.resources.requests.memory | string | `"500Mi"` | configures requests of RAM for "mongos" container in web application |
| nameOverride | string | `""` | is the string to partially override fullname template (will maintain the release name) and fully override name template. |
| newRelic.appId | string | `""` |  |
| newrelic.cronjobs | bool | `false` | Adds NewRelic PHP daemon sidecar container to CronJobs |
| newrelic.image | string | `"eu.gcr.io/autodoc-234411/newrelic/php-daemon:latest"` | NewRelic PHP daemon image name and version. Used in "newrelic" container of workers and cron jobs. |
| newrelic.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of NewRelic PHP daemon image. Possible values: "IfNotPresent", "Always" or "Never" |
| newrelic.newRelicConfigOverride.configPath | string | `"/usr/local/etc/php/conf.d/newrelic.ini"` | The NR ini config file location. |
| newrelic.newRelicConfigOverride.configVars | list | `[]` | The NR variables to be overridden. |
| newrelic.newRelicConfigOverride.cronjobs | bool | `false` | Mount the newrelic.ini ConfigMap to the cronjobs. Note: it will work only if '.Values.newrelic.cronjobs' is also 'true'. |
| newrelic.newRelicConfigOverride.enabled | bool | `false` | Enable the NR config override feature. |
| newrelic.newRelicConfigOverride.workers | bool | `false` | Mount the newrelic.ini ConfigMap to the workers. Note: it will work only if '.Values.newrelic.workers' is also 'true'. |
| newrelic.newRelicKeysManagedSecret.enabled | bool | `false` | Enable the built-in NR license and api keys managedSecret. Note: You are required to create a secret in GCP SM per GCP project with the following content:   NR_LICENSE_KEY={ Your license key }   NR_API_KEY={ Your api key }    |
| newrelic.newRelicKeysManagedSecret.gcpSmSecretName | string | `"new-relic-keys-prod"` | GCP SM secret name. |
| newrelic.resources.limits.memory | string | `"50Mi"` | configures limits of RAM for "newrelic" container |
| newrelic.resources.requests.cpu | string | `"50m"` | configures requests of CPU for "newrelic" container |
| newrelic.resources.requests.memory | string | `"50Mi"` | configures requests of RAM for "newrelic" container |
| newrelic.workers | bool | `false` | Adds NewRelic PHP daemon sidecar container to workers Deployments |
| nginx.additionalPvc | list | `[]` | Add additional shared volume (mounts directory from node) |
| nginx.config | string | `"server {\n  listen 80  default_server;\n  index      index.php index.html;\n  error_log  /dev/stderr warn;\n  access_log /dev/null;\n  root       /var/www/html/public;\n  location / {\n      try_files       $uri $uri/ /index.php?$query_string;\n  }\n  location = /favicon.ico {\n    try_files               $uri $uri/ /favicon.php;\n  }\n  location ~* \\.php$ {\n      try_files               $uri = 404;\n      fastcgi_pass            127.0.0.1:9000;\n      include                 fastcgi_params;\n      fastcgi_param           SCRIPT_FILENAME $document_root$fastcgi_script_name;\n      fastcgi_param           PATH_INFO $fastcgi_path_info;\n      fastcgi_param           HTTPS $http_x_forwarded_proto if_not_empty;\n      fastcgi_param           SERVER_PORT $http_x_forwarded_port;\n      fastcgi_param           HTTP_X_REQUEST_START \"t=${msec}\";\n      fastcgi_param           REMOTE_ADDR $http_x_real_ip;\n      fastcgi_hide_header     X-Powered-By;\n      fastcgi_read_timeout    6000;\n  }\n  location ~* \\.(jpg|jpeg|gif|png|bmp|swf|css|js|cur|(gz&!xml.gz)|pdf|img|ttf|woff|woff2|svg|lic)$ {\n      access_log              off;\n      expires                 360d;\n      add_header              Cache-Control public;\n  }\n  location /status {\n      stub_status;\n      auth_basic off;\n      allow all;\n  }\n  location ~ /\\. {\n      deny                    all;\n  }\n}\n"` | Nginx config file /etc/nginx/conf.d/default.conf |
| nginx.customConfig | object | `{"client_body_timeout":10,"keepalive_timeout":0,"worker_connections":4096}` | Nginx config file /etc/nginx/nginx.conf |
| nginx.customConfig.client_body_timeout | int | `10` | Defines a timeout for reading client request body. (https://nginx.org/en/docs/http/ngx_http_core_module.html#client_body_timeout) |
| nginx.enabled | bool | `true` | Enables adding of [Nginx](https://nginx.org/en/) sidecar container |
| nginx.image | string | `"eu.gcr.io/autodoc-234411/nginx:1.17"` | nginx image name and version. Used in "nginx" container of web application. |
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
| nginx.prepopulate | bool | `true` | If enabled uses shared volume for docroot |
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
| prescale | object | `{"backoffLimit":0,"defaultMinReplicas":40,"enabled":false,"git":{"hrsPath":"path/to/your/helm_release.yaml","repoUri":"git@gitlab.autodoc.dev:devops/helm-operator.git","sshKeySecret":"gitlab-private-ssh-key","userEmail":"autoscaler@autodoc.de","userName":"Prescaler"},"image":"gcr.io/autodoc-234411/helpers/helm:latest","imagePullSecrets":[],"items":[{"minReplicas":200,"name":"mon-1","schedule":"30 6 * * 1"}],"pullPolicy":"Always","resources":{"limits":{"memory":"500Mi"},"requests":{"cpu":"1","memory":"500Mi"}}}` | The "prescale" feature. Was developed in order to dynamically updating hpa object according to the crons defined into items key. Changes will be commited into git. |
| prescale.backoffLimit | int | `0` | Specify the number of retries before considering a prescale job as failed |
| prescale.defaultMinReplicas | int | `40` | Default value on hpa replicas for "down" job. |
| prescale.enabled | bool | `false` | Positive condition will create a list of job's pairs which will consist of two types of jobs - up and down. The "up" job will update parameter hpa.minReplicas according to the value defined in prescale.items[0].minReplicas.  The "down" job will reset that value back to prescale.defaultMinReplicas. |
| prescale.git | object | `{"hrsPath":"path/to/your/helm_release.yaml","repoUri":"git@gitlab.autodoc.dev:devops/helm-operator.git","sshKeySecret":"gitlab-private-ssh-key","userEmail":"autoscaler@autodoc.de","userName":"Prescaler"}` | List of git parameters in order to pull target hrs, make changes and push them. |
| prescale.git.hrsPath | string | `"path/to/your/helm_release.yaml"` | Path to the manifest file of target hrs. Must be written without root dir of git repo. |
| prescale.git.repoUri | string | `"git@gitlab.autodoc.dev:devops/helm-operator.git"` | Link to the target git repository. |
| prescale.git.sshKeySecret | string | `"gitlab-private-ssh-key"` | External secret for accessing to gitRepo which must be defined in addition and has to consist of "private-key-gitlab" key. |
| prescale.git.userEmail | string | `"autoscaler@autodoc.de"` | Git email. |
| prescale.git.userName | string | `"Prescaler"` | Git username. |
| prescale.image | string | `"gcr.io/autodoc-234411/helpers/helm:latest"` | Base helm image path. |
| prescale.imagePullSecrets | list | `[]` | Define the list of imagePullSecrets for prescale jobs, default secret won't be overwritten. |
| prescale.items | list | `[{"minReplicas":200,"name":"mon-1","schedule":"30 6 * * 1"}]` | List of job pairs. |
| prescale.pullPolicy | string | `"Always"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of prescale image. Possible values: "IfNotPresent", "Always" or "Never" |
| prescale.resources | object | `{"limits":{"memory":"500Mi"},"requests":{"cpu":"1","memory":"500Mi"}}` | Resources for jobs. |
| prescale.resources.limits.memory | string | `"500Mi"` | Memory limit.  |
| prescale.resources.requests.cpu | string | `"1"` | Cpu request. |
| prescale.resources.requests.memory | string | `"500Mi"` | Memory request. |
| prestop.command | list | `["/bin/bash","-c","/bin/sleep 10; kill -QUIT 1"]` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for app container |
| prometheusSD.enabled | bool | `false` |  |
| proxysql.appSecret | string | `""` | Add proxysql config for web application from secret |
| proxysql.cronSecret | string | `""` | Add proxysql config for cronjobs/workers from secret |
| proxysql.enabled | bool | `false` | Enables [ProxySQL](https://proxysql.com/) sidecar container |
| proxysql.image | string | `"eu.gcr.io/autodoc-234411/helpers/proxysql-optimize-log/proxysql:2.4.2"` | proxysql image name and version. Used in "proxysql" sidecar container of application. |
| proxysql.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of proxysql image. Possible values: "IfNotPresent", "Always" or "Never" |
| proxysql.initSlaves | object | `{"configPath":"/var/config/proxysql.override.cnf","enabled":false}` | Defines [Lifecycle poststart hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for proxysql container poststart:   command:   - /bin/bash   - -c   - /bin/sleep 10 |
| proxysql.initSlaves.configPath | string | `"/var/config/proxysql.override.cnf"` | Name of resulting proxysql config file |
| proxysql.initSlaves.enabled | bool | `false` | Enables "mysql-slaves" initContainer for slaves, which concatenates proxysql file containing passwords from Secret Manager with servers list in release |
| proxysql.login | string | `"pkwteile"` | Login for proxysql monitoring (monitor_username param) (DEPRECATED) |
| proxysql.mysql_users | string | `"{ username = \"pkwteile\" , password = \"ohheeRai4ea\" , default_hostgroup = 20 , active = 1 }\n"` | Proxysql users list (DEPRECATED). Moved to Secret Manager |
| proxysql.password | string | `"ohheeRai4ea"` | Password for proxysql monitoring (monitor_password param) (DEPRECATED) |
| proxysql.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for proxysql container |
| proxysql.resources.limits.memory | string | `"500Mi"` | configures limits of RAM for "proxysql" container |
| proxysql.resources.requests.cpu | string | `"100m"` | configures requests of CPU for "proxysql" container |
| proxysql.resources.requests.memory | string | `"500Mi"` | configures requests of RAM for "proxysql" container |
| proxysqlsession.appSecret | string | `""` | Add slaves proxysql config for web application from secret |
| proxysqlsession.cronSecret | string | `""` | Add slaves proxysql config for cronjobs/workers from secret |
| proxysqlsession.enabled | bool | `false` | Enables "proxysql-session" sidecar containerfor session slaves |
| proxysqlsession.image | string | `"eu.gcr.io/autodoc-234411/helpers/proxysql-optimize-log/proxysql:2.4.2"` | proxysql image name and version. Used in "proxysql-session" sidecar container of application. |
| proxysqlsession.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of proxysql image. Possible values: "IfNotPresent", "Always" or "Never" |
| proxysqlsession.initSlaves.configPath | string | `"/var/config/proxysqlsession.override.cnf"` | Name of resulting proxysql config file for session slaves |
| proxysqlsession.initSlaves.enabled | bool | `false` | Enables "mysql-session-slaves" initContainer for session slaves, which concatenates proxysql file containing passwords from Secret Manager with servers list in release |
| proxysqlsession.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for proxysqlsession container |
| proxysqlsession.resources.limits.memory | string | `"500Mi"` | configures limits of RAM for "proxysql-session" container |
| proxysqlsession.resources.requests.cpu | string | `"100m"` | configures requests of CPU for "proxysql-session" container |
| proxysqlsession.resources.requests.memory | string | `"500Mi"` | configures requests of RAM for "proxysql-session" container |
| proxysqlsession.servers | string | `"{}"` | Proxysql servers list of session slaves for web application |
| ramDocroot.enabled | bool | `false` | Creates shared volume in RAM for "app" and "nginx" containers |
| ramDocroot.size | string | `"2Gi"` | Defines RAM shared volume size |
| rbac.apiGroups | list | `[""]` | Specifies allowed apiGroups for Role/ClusterRole |
| rbac.enabled | bool | `false` | Enables [RBAC](https://cloud.google.com/kubernetes-engine/docs/how-to/role-based-access-control) for application. |
| rbac.existingRoleName | string | `""` | Allows existing Role/ClusterRole usage |
| rbac.level | string | `"namespace"` | Specifies the Role or ClusterRole object to be created. Possible values: namespace - Role object to be created. cluster - ClusterRole object to be created. |
| rbac.resources | list | `["*"]` | Specifies allowed resources for Role/ClusterRole |
| rbac.verbs | list | `["get","list"]` | Specifies allowed verbs for Role/ClusterRole |
| realeaseInfo.apiUrl | string | `"http://api.bison.local."` |  |
| realeaseInfo.enabled | bool | `true` |  |
| region | string | `"europe-west3"` | Used in "prometheus-to-sd" container of main Deployment |
| secret_env | object | `{"envs":[],"secretRef":"","secretRefNames":[]}` | Environment variable from an existing secret in "app" container |
| secret_env.envs | list | `[]` | array of variables names and secret's keys |
| secret_env.secretRef | string | `""` | existing secret name |
| secret_env.secretRefNames | list | `[]` | Please use secretRefNames for set existing secret's names |
| secretsManager.createEnvFile | bool | `false` | Create env file or only create environment variables |
| secretsManager.enabled | bool | `false` | Enables "secrets-manager" init container for getting secrets into pod (DEPRECATED). Please use ManagedSecret ([example](https://gitlab.autodoc.dev/infra/helm-operator/-/blob/main/infrastructure/shop-gclus-prod/prod/autodoc-corporate-service-account.yaml)) instead |
| secretsManager.image | string | `"eu.gcr.io/autodoc-234411/helpers/cloud-sdk:alpine"` | cloud-sdk image name and version. Used in "secrets-manager" container of application. |
| secretsManager.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of cloud-sdk image. Possible values: "IfNotPresent", "Always" or "Never" |
| secretsManager.name | string | `""` | GCP secret name |
| secretsManager.resources.limits.memory | string | `"100Mi"` | configures limits of RAM for "secrets-manager" container |
| secretsManager.resources.requests.cpu | string | `"50m"` | configures requests of CPU for "secrets-manager" container |
| secretsManager.resources.requests.memory | string | `"100Mi"` | configures requests of RAM for "secrets-manager" container |
| sellprice.SocketProxyAddr | string | `"/tmp/sellprice.sock"` | Configure SELLPRICE_UNIX_SOCKET_PROXY_ADDR environment variable |
| sellprice.competitorsCommunicationType | string | `"cache"` | Configure SELLPRICE_COMPETITORS_COMMUNICATION_TYPE environment variable |
| sellprice.competitorsHttpAddr | string | `""` | Configure SELLPRICE_COMPETITORS_HTTP_ADDR environment variable |
| sellprice.competitorsHttpToken | string | `""` | Configure SELLPRICE_COMPETITORS_HTTP_TOKEN environment variable |
| sellprice.connType | string | `"http"` | Configure SELLPRICE_CONNECTION_TYPE environment variable |
| sellprice.cronJobsPreStop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle cronJobsPreStop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) |
| sellprice.cronjobMetrics | object | `{"enabled":true,"service":{"annotations":{},"name":"sellprice","port":8081,"protocol":"TCP","targetPort":"sellprice","type":"NodePort"},"serviceMonitor":{"interval":"5s","labels":{},"scheme":"http","scrapeTimeout":"5s"}}` | Defines [Lifecycle cronJobsPostStart hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) cronJobsPostStart:    command: "ls -al /bin/" |
| sellprice.enablePriceBuilderFeature | string | `"true"` | Configure SELLPRICE_ENABLE_PRICE_BUILDER_FEATURE environment variable |
| sellprice.enabled | bool | `false` | Enable [Sellprice GRPC sidecar container](https://gitlab.autodoc.dev/ppm/sellprice/-/blob/master/Dockerfile.sidecar) |
| sellprice.grpcPool | string | `"false"` | Configure SELLPRICE_GRPC_POOL environment variable |
| sellprice.grpcPoolConnMax | string | `""` | Configure SELLPRICE_GRPC_POOL_CONN_MAX environment variable |
| sellprice.grpcPoolConnMin | string | `""` | Configure SELLPRICE_GRPC_POOL_CONN_MIN environment variable |
| sellprice.grpcPoolConnTll | string | `""` | Configure SELLPRICE_GRPC_POOL_CONN_TTL environment variable |
| sellprice.grpcTimeout | string | `"20000"` | Configure SELLPRICE_GRPC_TIMEOUT environment variable |
| sellprice.httpAddr | string | `":8081"` | Configure SELLPRICE_HTTP_ADDR environment variable |
| sellprice.httpProxyAddr | string | `":8081"` | TODO: deprecated |
| sellprice.image | string | `"europe-west3-docker.pkg.dev/dynamic-pricing-dd58/ppm/sellprice/prod/sidecar"` | TODO: change to europe-west3-docker.pkg.dev/dynamic-pricing-dd58/ppm/sellprice/prod/app after all clients will be moved to the new image |
| sellprice.logger | string | `"true"` | Configure SELLPRICE_LOGGER environment variable |
| sellprice.loggerFormatter | string | `"gcp"` | Configure SELLPRICE_LOGGER_FORMATTER environment variable |
| sellprice.loggerLevel | string | `"info"` | Configure SELLPRICE_LOGGER_LEVEL environment variable |
| sellprice.metrics | bool | `true` | Enable exporting port 8081 of pod and additional ServiceMonitor object  |
| sellprice.natsPassword | string | `""` | Configure SELLPRICE_NATS_PASS environment variable |
| sellprice.natsUrl | string | `""` | Configure SELLPRICE_NATS_URL environment variable |
| sellprice.natsUser | string | `""` | Configure SELLPRICE_NATS_USER environment variable |
| sellprice.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for sellprice container |
| sellprice.rcCommunicationType | string | `"cache"` | Configure SELLPRICE_RC_COMMUNICATION_TYPE environment variable |
| sellprice.rcTcpAddr | string | `""` | Configure SELLPRICE_RC_TCP_ADDR environment variable |
| sellprice.redisAddr | string | `""` | Configure SELLPRICE_REDIS_ADDR environment variable |
| sellprice.redisDbParams | string | `"1"` | Configure SELLPRICE_REDIS_DB_PARAMS environment variable |
| sellprice.redisDbe | string | `"0"` | Configure SELLPRICE_REDIS_DB environment variable |
| sellprice.redisPassword | string | `""` | Configure SELLPRICE_REDIS_PASSWORD environment variable |
| sellprice.resources.limits.memory | string | `"100Mi"` | configures limits of RAM for "sellprice" container in web application |
| sellprice.resources.requests.cpu | string | `"50m"` | configures requests of CPU for "sellprice" container in web application |
| sellprice.resources.requests.memory | string | `"100Mi"` | configures requests of RAM for "sellprice" container in web application |
| sellprice.tag | string | `"latest"` | mongos image version. Used in "sellprice" sidecar container of application. |
| sellprice.tcpAddr | string | `":9091"` | Configure SELLPRICE_TCP_ADDR environment variable |
| sellprice.tcpProxyAddr | string | `":9091"` | TODO: deprecated |
| sellprice.tracer | string | `""` | Configure SELLPRICE_TRACER environment variable |
| sellprice.tracerCredentialsFile | string | `""` | Configure SELLPRICE_TRACER_CREDENTIALS_FILE environment variable |
| sellprice.tracerGcpPid | string | `""` | Configure SELLPRICE_TRACER_GCP_PID environment variable |
| sellprice.tracerGcpSampleRatio | string | `""` | Configure SELLPRICE_TRACER_GCP_SAMPLER_RATIO environment variable |
| sellprice.tracerServiceName | string | `""` | Configure SELLPRICE_TRACER_SERVICE_NAME environment variable |
| sellprice.workerMetrics.enabled | bool | `true` |  |
| sellprice.workerMetrics.service.annotations | object | `{}` |  |
| sellprice.workerMetrics.service.name | string | `"sellprice"` |  |
| sellprice.workerMetrics.service.port | int | `8081` |  |
| sellprice.workerMetrics.service.protocol | string | `"TCP"` |  |
| sellprice.workerMetrics.service.targetPort | string | `"sellprice"` |  |
| sellprice.workerMetrics.service.type | string | `"NodePort"` |  |
| sellprice.workerMetrics.serviceMonitor.interval | string | `"10s"` |  |
| sellprice.workerMetrics.serviceMonitor.labels | object | `{}` |  |
| sellprice.workerMetrics.serviceMonitor.scheme | string | `"http"` |  |
| sellprice.workerMetrics.serviceMonitor.scrapeTimeout | string | `"10s"` |  |
| sellprice.workerPreStop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle workerPreStop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) |
| service.enabled | bool | `true` | Enables Kubernetes [Service object](https://kubernetes.io/docs/concepts/services-networking/service/) creation |
| service.extraServicePorts | list | `[]` | extra port for service |
| service.loadBalancerSourceRanges | list | `["127.0.0.1/32","10.0.0.0/8"]` | In order to limit which client IP's can access the Network Load Balancer, specify loadBalancerSourceRanges. |
| service.name | string | `"http-web"` | Name of port in service |
| service.port | int | `80` | Defines Service port number |
| service.protocol | string | `"TCP"` | Defines Service port's protocol |
| service.targetName | string | `"http"` | Name of port in pod |
| service.type | string | `"NodePort"` | Defines Service type Possible values: "NodePort", "ClusterIP", "LoadBalancer" or "ExternalName" |
| serviceMonitor.enabled | bool | `false` | If true, a ServiceMonitor CRD is created for a prometheus operator https://github.com/coreos/prometheus-operator |
| serviceMonitor.endpoints | list | `[{"honorLabels":true,"interval":"10s","metricRelabelings":[],"path":"/metrics","port":"http-metrics","relabelings":[{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_pod_label_app"],"targetLabel":"app"},{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_namespace"],"targetLabel":"branch"}],"scheme":"http","scrapeTimeout":"10s"}]` | ServiceMonitor endpoint path |
| serviceMonitor.endpoints[0] | object | `{"honorLabels":true,"interval":"10s","metricRelabelings":[],"path":"/metrics","port":"http-metrics","relabelings":[{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_pod_label_app"],"targetLabel":"app"},{"action":"replace","regex":"^(.*)$","replacement":"$1","separator":";","sourceLabels":["__meta_kubernetes_namespace"],"targetLabel":"branch"}],"scheme":"http","scrapeTimeout":"10s"}` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).relabelings param of ServiceMonitor object. [Relabelings vs metricRelabelings](https://github.com/prometheus-operator/prometheus-operator/issues/3246) |
| serviceMonitor.externalExporter | bool | `true` | Enable "monitoring" sidecar container |
| serviceMonitor.image | string | `"eu.gcr.io/autodoc-234411/php-fpm_exporter:1.0.0"` | [php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) image name and version. Used in "monitoring" sidecar container of application. |
| serviceMonitor.interval | string | `"10s"` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).interval param of ServiceMonitor object |
| serviceMonitor.labels | object | `{}` | Labels added to ServiceMonitor object |
| serviceMonitor.metricRelabelings | list | `[]` | [endpoints](https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#endpoint).metricRelabelings param of ServiceMonitor object. [Relabelings vs metricRelabelings](https://github.com/prometheus-operator/prometheus-operator/issues/3246) |
| serviceMonitor.metricsPort | int | `9253` | Monitoring Port to be exported by Service |
| serviceMonitor.promToSdImage | string | `"eu.gcr.io/autodoc-234411/prometheus-to-sd:v0.9.2"` | [prometheus-to-sd](https://github.com/GoogleCloudPlatform/k8s-stackdriver/tree/master/prometheus-to-sd) image name and version. Used in the "prometheus-to-sd" sidecar container of application. |
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
| twemproxy.config | object | `{"alpha":{"auto_eject_hosts":false,"distribution":"ketama","hash":"fnv1a_64","hash_tag":"{}","listen":"/tmp/redis.sock 0666","redis":true,"servers":["10.185.57.164:6379:1 server1"]}}` | Config for twemproxy app |
| twemproxy.enabled | bool | `false` | Enables [twemproxy](https://github.com/twitter/twemproxy) sidecar container |
| twemproxy.image | string | `"eu.gcr.io/autodoc-234411/twemproxy:0.5.0"` | twemproxy image name and version. Used in the "twemproxy" sidecar container of application. |
| twemproxy.imagePullPolicy | string | `"IfNotPresent"` | specifies an [imagePullPolicy](http://kubernetes.io/docs/user-guide/images/#updating-images) of twemproxy image. Possible values: "IfNotPresent", "Always" or "Never" |
| twemproxy.prestop | object | `{"command":["/bin/bash","-c","/bin/sleep 10"]}` | Defines [Lifecycle prestop hook](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) for twemproxy container |
| twemproxy.resources.limits.memory | string | `"300Mi"` | configures limits of RAM for "twemproxy" container in web application |
| twemproxy.resources.requests.cpu | string | `"300m"` | configures requests of CPU for "twemproxy" container in web application |
| twemproxy.resources.requests.memory | string | `"300Mi"` | configures requests of RAM for "twemproxy" container in web application |
| updater.branch | string | `"test"` | Branch of git repository to be used during initial "git clone" and "git pull" in loop. |
| updater.copyDirs | list | `["vendor"]` | List of directories to be copied to docroot from /app additionally |
| updater.customCommands | list | `[]` | List of commands to be executed in "data" initContainer and "updater" container after "composer install" |
| updater.debug | bool | `false` | Controls debug information in "data" initContainer's logs. |
| updater.enabled | bool | `false` | Changes "data" initContainer behavior - "data" initContainer populate data with "git clone" instead of copying from /app dir. Creates sidecar container "updater" with "git pull" in loop, and runs some additional commands like "composer update". |
| updater.repository | string | `""` | Git repository to be used during initial "git clone" and "git pull" in loop. |
| updater.resources.limits.memory | string | `"3Gi"` | configures limits of RAM for "updater" container |
| updater.resources.requests.cpu | string | `"1"` | configures requests of CPU for "updater" container |
| updater.resources.requests.memory | string | `"3Gi"` | configures requests of RAM for "updater" container |
| vpa | object | `{"enabled":false,"maxAllowed":{"memory":"500Mi"},"minAllowed":{"memory":"100Mi"},"updateMode":"Auto"}` | configures vertical pod autoscale |
| vpa.maxAllowed | object | `{"memory":"500Mi"}` | configure maximum allowed memory for vpa |
| vpa.minAllowed | object | `{"memory":"100Mi"}` | configure minimal allowed memory for vpa |
| workers | list | `[]` | Array of workers [Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) |