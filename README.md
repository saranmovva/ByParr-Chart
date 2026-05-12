# ByParr Helm Chart

Helm chart for [Byparr](https://github.com/ThePhaseless/Byparr) — a drop-in replacement for FlareSolverr using [Camoufox](https://github.com/daijro/camoufox) to bypass Cloudflare and DDoS-Guard challenges.

## Prerequisites

- Kubernetes 1.21+
- Helm 3.8+ (OCI registry support required)

## Installation

### Add and install from OCI registry

```sh
helm install byparr oci://ghcr.io/saranmovva/charts/byparr
```

### Install a specific version

```sh
helm install byparr oci://ghcr.io/saranmovva/charts/byparr --version 0.1.1
```

### Install with custom values

```sh
helm install byparr oci://ghcr.io/saranmovva/charts/byparr -f values.yaml
```

## Pulling the chart

```sh
helm pull oci://ghcr.io/saranmovva/charts/byparr
# or pull and untar a specific version
helm pull oci://ghcr.io/saranmovva/charts/byparr --version 0.1.1 --untar
```

## Upgrading

```sh
helm upgrade byparr oci://ghcr.io/saranmovva/charts/byparr
```

## Uninstalling

```sh
helm uninstall byparr
```

## Configuration

The following table lists the key configurable parameters.

| Parameter | Description | Default |
|---|---|---|
| `image.repository` | Byparr image repository | `ghcr.io/thephaseless/byparr` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.main.ports.main.port` | Service port | `8191` |

To see all available values:

```sh
helm show values oci://ghcr.io/saranmovva/charts/byparr
```

## Usage with *arr apps

Byparr is API-compatible with FlareSolverr. Point your \*arr application's FlareSolverr URL to:

```
http://byparr:8191
```

## Source

- Chart: [github.com/saranmovva/ByParr-Chart](https://github.com/saranmovva/ByParr-Chart)
- Upstream app: [github.com/ThePhaseless/Byparr](https://github.com/ThePhaseless/Byparr)
