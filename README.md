# Exporting all telemetry data from OpenShift via OpenTelemetry protocol (OTLP)

This repository contains guides how to setup OpenTelemetry collector to export (all) telemetry data
from OpenShift.

## Metrics

For exporting metrics Prometheus receiver can be setup to scrape `/federate` endpoint from in-cluster
monitoring  and user-workload monitoring stacks.

## Logs

TBD.

The idea is to configure Vector with Vector Remap Language ([VRL](https://vector.dev/docs/reference/vrl/)) to transform data to OTLP JSON and send it to OTLLP HTTP/json receiver on the collector.

* OTLP JSON examples https://github.com/open-telemetry/opentelemetry-proto/blob/main/examples/README.md
* https://github.com/jcantrill/cluster-logging-operator/blob/log4531/internal/generator/vector/conf_test/complex_otel.toml
* https://github.com/jcantrill/cluster-logging-operator/blob/log4531/internal/generator/vector/normalize/schema/otel/transform.go#L23
* `~/projects/openshift/cluster-logging-operator/test/functional/normalization/schema (log4531*) » KUBECONFIG=${HOME}/.kube/config  RELATED_IMAGE_VECTOR=quay.io/openshift-logging/vector:5.8.0 go test --tags=vector  ./... `
*  https://github.com/pavolloffay/cluster-logging-operator/tree/log4531-pavol recording https://vimeo.com/manage/videos/912553320/2f71aa6874?extension_recording=true
* there are containers `http` (otelcol) and `collector` (vector)
* https://issues.redhat.com/browse/LOG-4531 and https://github.com/jcantrill/cluster-logging-operator/tree/log4531

## Tracing

For tracing no additional configuration is required. Exported traces from workload are pushed to the collector.
