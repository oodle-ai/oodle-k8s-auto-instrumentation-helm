# Oodle auto-instrumentation helm chart.

## Introduction
Auto-instrument your kubernetes cluster using eBPF agents and
analyze the data using Oodle.

## Installation
Create a `values.yaml` file similar to the [example-values.yaml](./example-values.yaml)

```bash
cat > values.yaml << EOF
beyla:
  resources:
    limits:
      memory: 4Gi
    requests:
      cpu: 100m
      memory: 1Gi
  env:
    OTEL_EXPORTER_OTLP_METRICS_ENDPOINT: "{OODLE_ENDPOINT}"
    OTEL_EXPORTER_OTLP_HEADERS: "X-API-KEY={OODLE_API_KEY}"
    BEYLA_KUBE_CLUSTER_NAME: "{KUBE_CLUSTER_NAME}"

    BEYLA_NAME_RESOLVER_SOURCES: "k8s,dns"
EOF
```

Run the following helm command to start sending data to Oodle.
```bash
helm repo add --force-update oodle https://oodle-ai.github.io/helm-charts;
helm upgrade --install oodle-k8s-auto-instrumentation oodle/oodle-k8s-auto-instrumentation --values values.yaml --namespace oodle-instrumentation --create-namespace
```

