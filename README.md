# GitOps Repository

## Structure

- `root.yaml` - Bootstrap application (App of Apps)
- `manifests/` - ArgoCD Application definitions organized by component type
- `apps/` - Actual Kubernetes manifests

## Component Types

1. **Infrastructure** - Core cluster components (Traefik, cert-manager, MetalLB)
2. **Databases** - Data stores (PostgreSQL, Redis, MongoDB)
3. **Monitoring** - Observability stack (Prometheus, Grafana, Loki)
4. **Services** - Application services

## Deployment Order (Sync Waves)

1. Wave 1: Infrastructure basics (cert-manager, MetalLB)
2. Wave 2: Ingress (Traefik)
3. Wave 3: Databases
4. Wave 4: Monitoring
5. Wave 5: Services

## Bootstrap

```bash
kubectl apply -f root.yaml
```

## Adding New Applications

1. Create manifest files in `apps/<component-type>/<app-name>/`
2. Create Application definition in `manifests/<component-type>/<app-name>.yaml`
3. Commit and push - ArgoCD will auto-deploy

## Removing Applications

1. Delete files from `manifests/<component-type>/<app-name>.yaml`
2. Commit and push - ArgoCD will auto-prune
