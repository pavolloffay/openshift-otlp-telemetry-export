# Logging

Manifests in this directory configure OCP logging stack (CLO/Vector with Loki) and
OpenTelemetry collector that sends data to the same Loki instance as `application` tenant.


## LogCLI

```bash
kubectl get route lokistack-dev -o jsonpath="{.spec.host}" -n openshift-logging
logcli --tls-skip-verify --bearer-token="$(oc whoami -t)" --addr "https://logging-loki-openshift-logging.apps-crc.testing/api/logs/v1/application" labels
logcli --tls-skip-verify --bearer-token="$(oc whoami -t)" --addr "https://logging-loki-openshift-logging.apps-crc.testing/api/logs/v1/application" labels  collector_type
logcli --tls-skip-verify --bearer-token="$(oc whoami -t)" --addr "https://logging-loki-openshift-logging.apps-crc.testing/api/logs/v1/application" query '{kubernetes_namespace_name="tutorial-application"}'
logcli --tls-skip-verify --bearer-token="$(oc whoami -t)" --addr "https://logging-loki-openshift-logging.apps-crc.testing/api/logs/v1/application" query '{level="INFO"}' 
```