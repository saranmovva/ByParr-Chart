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
| `ingress.main.enabled` | Enable ingress | `false` |
| `ingress.main.ingressClassName` | Ingress class name | `""` |
| `ingress.main.hosts[0].host` | Hostname | `byparr.example.com` |
| `ingress.main.tls` | TLS configuration | `[]` |
| `ingress.main.integrations.traefik.enabled` | Enable Traefik integration | `false` |
| `ingress.main.integrations.nginx.enabled` | Enable NGINX integration | `false` |
| `ingress.main.integrations.certManager.enabled` | Enable cert-manager integration | `false` |

To see all available values:

```sh
helm show values oci://ghcr.io/saranmovva/charts/byparr
```

## Ingress

Ingress is disabled by default. To enable it, override the following in your values file:

```yaml
ingress:
  main:
    enabled: true
    ingressClassName: "nginx"  # or "traefik", etc.
    hosts:
      - host: byparr.example.com
        paths:
          - path: /
            pathType: Prefix
    tls:
      - hosts:
          - byparr.example.com
        secretName: byparr-tls
```

### With cert-manager

```yaml
ingress:
  main:
    enabled: true
    ingressClassName: "nginx"
    hosts:
      - host: byparr.example.com
        paths:
          - path: /
            pathType: Prefix
    integrations:
      certManager:
        enabled: true
        certificateIssuer: letsencrypt-prod
```

### With Traefik

```yaml
ingress:
  main:
    enabled: true
    hosts:
      - host: byparr.example.com
    integrations:
      traefik:
        enabled: true
```

## Usage with *arr apps

Byparr is API-compatible with FlareSolverr. Point your \*arr application's FlareSolverr URL to:

```
http://byparr:8191
```

## Source

- Chart: [github.com/saranmovva/ByParr-Chart](https://github.com/saranmovva/ByParr-Chart)
- Upstream app: [github.com/ThePhaseless/Byparr](https://github.com/ThePhaseless/Byparr)
