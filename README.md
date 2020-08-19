# Helm Chart for Adminer

[![CircleCI](https://circleci.com/gh/cetic/helm-adminer.svg?style=svg)](https://circleci.com/gh/cetic/helm-adminer/tree/master) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![version](https://img.shields.io/github/tag/cetic/helm-adminer.svg?label=release)

## Introduction

This [Helm](https://github.com/kubernetes/helm) chart installs [Adminer](https://www.adminer.org) in a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster 1.10+
- Helm 3.0.0+
- PV provisioner support in the underlying infrastructure.

## Installation

### Add Helm repository

```bash
helm repo add cetic https://cetic.github.io/helm-charts
helm repo update
```

### Configure the chart

The following items can be set via `--set` flag during installation or configured by editing the `values.yaml` directly (need to download the chart first).

#### Configure the way how to expose Adminer service:

- **Ingress**: The ingress controller must be installed in the Kubernetes cluster.
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster.
- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). You’ll be able to contact the NodePort service, from outside the cluster, by requesting `NodeIP:NodePort`.
- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer.

### Install the chart

Install the Adminer helm chart with a release name `my-release`:

```bash
helm install --name my-release cetic/adminer
```

## Uninstallation

To uninstall/delete the `my-release` deployment:

```bash
helm delete --purge my-release
```

## Configuration

The following table lists the configurable parameters of the Adminer chart and the default values.

| Parameter                         | Description                                                             | Default                     |
| --------------------------------- | ----------------------------------------------------------------------- | --------------------------- |
| **Image**                                                                                                                                 |
| `image.repository`                | Image                                                                   | `adminer`                   |
| `image.tag`                       | Image tag                                                               | `4.7.7-standalone`          |
| `image.pullPolicy`                | Image pull policy                                                       | `IfNotPresent`              |
| `image.pullSecrets`               | Image pull secrets for private registry                                 | `[]`              |
| **Config**                                                                                                                                |
| `config.plugins`                  | List of plugins to install. You can find the list of plugins on [GitHub](https://github.com/vrana/adminer/tree/master/plugins)| ``|
| `config.design`                   | A bundled design to use. You can find the list of designs on [GitHub](https://github.com/vrana/adminer/tree/master/designs)| ``|
| `config.externalserver`           | The default host                                                        | ``                          |
| **Service**                                                                                                                               |
| `service.type`                    | Service type                                                            | `NodePort`                  |
| `service.port`                    | The service port                                                        | `80`                        |
| `service.annotations`             | Custom annotations for service                                          | `{}`                        |
| `service.labels`                  | Additional custom labels for the service                                | `{}`                        |
| `service.loadBalancerIP`          | LoadBalancerIP if service type is `LoadBalancer`                        | `nil`                       |
| `service.loadBalancerSourceRanges`| Address that are allowed when svc is `LoadBalancer`                     | `[]`                        |
| **Ingress**                                                                                                                               |
| `ingress.enabled`                 | Enables Ingress                                                         | `false`                     |
| `ingress.annotations`             | Ingress annotations                                                     | `{}`                        |
| `ingress.labels`                  | Custom labels                                                           | `{}`                        |
| `ingress.hosts`                   | Ingress accepted hostnames                                              | `[]`                        |
| `ingress.tls`                     | Ingress TLS configuration                                               | `[]`                        |
| **Resources**                                                                                                                             |
| `resources`                       | CPU/Memory resource requests/limits                                     | `{}`                        |
| **Tolerations**                                                                                                                           |
| `tolerations`                     | Add tolerations                                                         | `[]`                        |
| **NodeSelector**                                                                                                                          |
| `nodeSelector`                    | node labels for pod assignment                                          | `{}`                        |
| **Affinity**                                                                                                                              |
| `affinity`                        | node/pod affinities                                                     | `{}`                        |
| **LivenessProbe**                                                                                                                         |
| `livenessProbe`                   | Liveness probe settings                                                 | `nil`                        |
| **ReadnessProbe**                                                                                                                         |
| `readinessProbe`                  | Readiness probe settings                                                | `nil`                        |

## Credits

Initially inspired from https://github.com/mogaal/helm-charts/tree/master/adminer.

## Contributing

Feel free to contribute by making a [pull request](https://github.com/cetic/helm-adminer/pull/new/master).

Please read the official [Contribution Guide](https://github.com/helm/charts/blob/master/CONTRIBUTING.md) from Helm for more information on how you can contribute to this Chart.

## License

[Apache License 2.0](/LICENSE.md)

