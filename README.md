#Flux Demo App

This is a basic flux v2 deployment for a demo application on a KIND Cluster.

## Bootstrap

The deployment files are kept under `./clusters/ko2/` directory.

To bootstrap the fluxcd deployment issue:

```
flux bootstrap github --components-extra=image-reflector-controller,image-automation-controller --owner=debuggerboy --repository=ko2-infra --branch=main --path=clusters/ko2 --token-auth
```

This will prompt for GH PAT, provide the same.

## Ingress Nginx

The ingress-nginx ingress controller can be found in `./clusters/ko2/ingress-nginx/` directory.

The bootstrap will install the ingress-nginx ingress controller into the KIND kubernetes cluster.

To verify the ingress controller is online issue:

```
kubectl wait --for=condition=Ready pod -l app.kubernetes.io/component=controller -n ingress-nginx --timeout=300s
```

```
kubectl wait --for=condition=Complete job -l app.kubernetes.io/component=admission-webhook -n ingress-nginx --timeout=300s
```
