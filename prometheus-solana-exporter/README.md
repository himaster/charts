# Prometheus Solana Exporter

A Prometheus exporter for [Solana](https://solana.com/) metrics.

This chart creates a [Solana Exporter](https://github.com/certusone/solana_exporter) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.9+ with Beta APIs enabled
- Helm 3

## Get Repository Info

<!-- textlint-disable terminology -->
```console
helm repo add charts https://github.com/himaster/charts
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._
<!-- textlint-enable -->

## Install Chart

```console
helm install [RELEASE_NAME] charts/prometheus-solana-exporter
```

_See [configuration](#configuration) below._

_See [helm install](https://helm.sh/docs/helm/helm_install/) for command documentation._

## Uninstall Chart

```console
helm uninstall [RELEASE_NAME]
```

This removes all the Kubernetes components associated with the chart and deletes the release.

_See [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/) for command documentation._

## Upgrading Chart

```console
helm upgrade [RELEASE_NAME] [CHART] --install
```

_See [helm upgrade](https://helm.sh/docs/helm/helm_upgrade/) for command documentation._

## Configuration

See [Customizing the Chart Before Installing](https://helm.sh/docs/intro/using_helm/#customizing-the-chart-before-installing). To see all configurable options with detailed comments, visit the chart's [values.yaml](./values.yaml), or run these configuration commands:

```console
helm show values charts/prometheus-solana-exporter
```

### Solana Server Info

Set `solanaServer` to `http://[MY_SOLANA_HOST]:[MY_SOLANA_PORT]`.

### Flags

Check the [Flags](https://github.com/certusone/solana_exporter/tree/master#command-line-arguments) list and add to the `options` block in your value overrides.
