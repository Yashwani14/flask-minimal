# Flask Minimal Helm Chart

A Helm chart for deploying the Flask minimal application to Kubernetes.

## Installation

### Prerequisites
- Kubernetes cluster
- Helm 3.0+

### Install the Chart

```bash
# Install with default values
helm install flask-minimal ./helm

# Install with custom release name
helm install my-flask ./helm

# Install with custom values
helm install flask-minimal ./helm -f custom-values.yaml
```

### Uninstall the Chart

```bash
helm uninstall flask-minimal
```

## Configuration

The following table lists the configurable parameters of the Flask Minimal chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `2` |
| `image.repository` | Container image repository | `acrcreate.azurecr.io/flask-minimal` |
| `image.tag` | Container image tag | `v1` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Service type | `LoadBalancer` |
| `service.port` | Service port | `80` |
| `service.targetPort` | Container target port | `8080` |
| `resources.limits.cpu` | CPU limit | `500m` |
| `resources.limits.memory` | Memory limit | `512Mi` |
| `resources.requests.cpu` | CPU request | `250m` |
| `resources.requests.memory` | Memory request | `256Mi` |
| `probes.readiness.enabled` | Enable readiness probe | `true` |
| `probes.liveness.enabled` | Enable liveness probe | `true` |

### Example Values

```yaml
# Scale the deployment
replicaCount: 3

# Custom image settings
image:
  repository: your-registry/flask-minimal
  tag: v2
  pullPolicy: Always

# Use NodePort instead of LoadBalancer
service:
  type: NodePort
  port: 8080
  targetPort: 8080

# Custom resource limits
resources:
  limits:
    cpu: 1000m
    memory: 1Gi
  requests:
    cpu: 500m
    memory: 512Mi
```

## Usage

### Deploy with custom values

```bash
helm install flask-minimal ./helm \
  --set replicaCount=3 \
  --set image.tag=v2 \
  --set service.type=NodePort
```

### Verify installation

```bash
# Check deployment
kubectl get deployment
kubectl get pods
kubectl get svc

# View deployment details
helm status flask-minimal
helm get values flask-minimal
```

### Upgrade the deployment

```bash
helm upgrade flask-minimal ./helm --set image.tag=v2
```
