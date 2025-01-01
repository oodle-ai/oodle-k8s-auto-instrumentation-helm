# Oodle auto-instrumentation helm chart.

## Introduction
Auto-instrument your kubernetes cluster using eBPF agents and
analyze the data using Oodle.

## Installation
Create a `values.yaml` file similar to the [example-values.yaml](./example-values.yaml)

```bash
cat > values.yaml << EOF
alloy:
  alloy:
    extraEnv:
      - name: OODLE_REMOTE_WRITE_ENDPOINT
        value: "{OODLE_ENDPOINT}"
      - name: OODLE_REMOTE_WRITE_API_KEY
        value: "{OODLE_API_KEY}"
EOF
```

Run the following helm command to start sending data to Oodle.
```bash
helm upgrade --install oodle/oodle-k8s-auto-instrumentation --values values.yaml --namespace oodle-instrumentation --create-namespace
```

