# Dify Helm Chart

This Helm chart deploys [Dify](https://dify.ai/), an open-source LLMOps platform, on a Kubernetes cluster.

## Introduction

Dify is a LLM Application Development Platform. It integrates the best LLM application development practices, helping developers focus more on product features and business logic rather than LLM prompts and complex workflows.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure (if persistence is needed)

## Installing the Chart

### Option 1: Install from Helm Repository (Recommended)

```bash
# Add the Helm repository
helm repo add dify-chart https://daocloud.github.io/dify-chart
helm repo update

# Install the chart
helm install dify dify-chart/dify-chart

# Install with custom namespace
helm install dify dify-chart/dify-chart --namespace dify --create-namespace
```

### Option 2: Install from Local Directory

```bash
# Clone the repository
git clone https://github.com/DaoCloud/dify-chart.git
cd dify-chart

# Install the chart
helm install dify ./dify-chart

# Install with custom namespace
helm install dify ./dify-chart --namespace dify --create-namespace
```

## Uninstalling the Chart

To uninstall/delete the `dify` deployment:

```bash
helm delete dify
```

## Configuration

The following table lists the configurable parameters of the Dify chart and their default values.

| Parameter                         | Description                                                  | Default                    |
| --------------------------------- | ------------------------------------------------------------ | -------------------------- |
| `global.environment`              | Environment name                                             | `production`               |
| `global.storage.type`             | Storage type (hostPath or PVC)                               | `hostPath`                 |
| `global.storage.hostPath.basePath`| Base path for hostPath volumes                               | `/root/dify`               |
| `image.registry`                  | Global default image registry                                | `docker.m.daocloud.io`     |
| `image.pullPolicy`                | Image pull policy                                            | `IfNotPresent`             |
| `credentials.postgres.username`   | PostgreSQL username                                          | `postgres`                 |
| `credentials.postgres.password`   | PostgreSQL password                                          | `difyai123456`             |
| `credentials.postgres.database`   | PostgreSQL database name                                     | `dify`                     |
| `credentials.redis.username`      | Redis username                                               | `""`                       |
| `credentials.redis.password`      | Redis password                                               | `difyai123456`             |
| `credentials.weaviate.apiKey`     | Weaviate API key                                             | `WVF5YThaHlkYwhGUSmCRgsX3tD5ngdN8pkih` |
| `api.image.registry`              | API server image registry                                    | `docker.m.daocloud.io`     |
| `api.image.repository`            | API server image repository                                  | `langgenius/dify-api`      |
| `api.image.tag`                   | API server image tag                                         | `0.15.2`                   |
| `api.replicas`                    | Number of API server replicas                                | `1`                        |
| `api.resources`                   | API server resource requests and limits                      | See values.yaml            |
| `api.secretKey`                   | API server secret key                                        | `sk-9f73s3ljTXVcMT3Blb3ljTqtsKiGHXVcMT3BlbkFJLK7U` |
| `worker.image.registry`           | Worker image registry                                        | `docker.m.daocloud.io`     |
| `worker.image.repository`         | Worker image repository                                      | `langgenius/dify-api`      |
| `worker.image.tag`                | Worker image tag                                             | `0.15.2`                   |
| `worker.replicas`                 | Number of worker replicas                                    | `1`                        |
| `worker.resources`                | Worker resource requests and limits                          | See values.yaml            |
| `web.image.registry`              | Web frontend image registry                                  | `docker.m.daocloud.io`     |
| `web.image.repository`            | Web frontend image repository                                | `langgenius/dify-web`      |
| `web.image.tag`                   | Web frontend image tag                                       | `0.15.2`                   |
| `web.replicas`                    | Number of web frontend replicas                              | `1`                        |
| `web.resources`                   | Web frontend resource requests and limits                    | See values.yaml            |
| `postgres.image.registry`         | PostgreSQL image registry                                    | `docker.m.daocloud.io`     |
| `postgres.image.repository`       | PostgreSQL image repository                                  | `postgres`                 |
| `postgres.image.tag`              | PostgreSQL image tag                                         | `15-alpine`                |
| `postgres.resources`              | PostgreSQL resource requests and limits                      | See values.yaml            |
| `redis.image.registry`            | Redis image registry                                         | `docker.m.daocloud.io`     |
| `redis.image.repository`          | Redis image repository                                       | `redis`                    |
| `redis.image.tag`                 | Redis image tag                                              | `6-alpine`                 |
| `redis.resources`                 | Redis resource requests and limits                           | See values.yaml            |
| `weaviate.image.registry`         | Weaviate image registry                                      | `docker.m.daocloud.io`     |
| `weaviate.image.repository`       | Weaviate image repository                                    | `semitechnologies/weaviate`|
| `weaviate.image.tag`              | Weaviate image tag                                           | `1.19.0`                   |
| `weaviate.resources`              | Weaviate resource requests and limits                        | See values.yaml            |
| `sandbox.image.registry`          | Sandbox image registry                                       | `docker.m.daocloud.io`     |
| `sandbox.image.repository`        | Sandbox image repository                                     | `langgenius/dify-sandbox`  |
| `sandbox.image.tag`               | Sandbox image tag                                            | `0.2.10`                   |
| `sandbox.resources`               | Sandbox resource requests and limits                         | See values.yaml            |
| `sandbox.apiKey`                  | Sandbox API key                                              | `dify-sandbox`             |
| `ssrf.image.registry`             | SSRF proxy image registry                                    | `docker.m.daocloud.io`     |
| `ssrf.image.repository`           | SSRF proxy image repository                                  | `ubuntu/squid`             |
| `ssrf.image.tag`                  | SSRF proxy image tag                                         | `latest`                   |
| `ssrf.resources`                  | SSRF proxy resource requests and limits                      | See values.yaml            |
| `nginx.image.registry`            | Nginx image registry                                         | `docker.m.daocloud.io`     |
| `nginx.image.repository`          | Nginx image repository                                       | `nginx`                    |
| `nginx.image.tag`                 | Nginx image tag                                              | `stable`                   |
| `nginx.resources`                 | Nginx resource requests and limits                           | See values.yaml            |
| `nginx.service.type`              | Nginx service type                                           | `NodePort`                 |
| `nginx.service.nodePort`          | Nginx service NodePort                                       | `30000`                    |
| `persistence.enabled`             | Enable persistence storage                                   | `true`                     |

## Storage

By default, the chart uses `hostPath` for storage. This is suitable for single-node clusters or testing environments. For production, you should change `global.storage.type` to use persistent volumes.

## Security

Note that this chart contains default credentials that should be changed before deploying to production. Update the following values:

- `credentials.postgres.password`
- `credentials.redis.password`
- `credentials.weaviate.apiKey`
- `api.secretKey`
- `sandbox.apiKey`

## License

This chart is licensed under the same terms as Dify itself. See the [Dify license](https://github.com/langgenius/dify/blob/main/LICENSE) for details. 