# Sample-argo

sample chart for argo issue

## Step

1. deploy parent application

```cmd
kubectl apply -f application.yaml
```

2. change child application chart's targetRevision

```yaml
project: default
destination:
  server: https://kubernetes.default.svc
  namespace: argo
syncPolicy:
  syncOptions:
    - CreateNamespace=true
sources:
  - repoURL: https://github.com/kahmnkk/sample-argo.git
    path: child/
    targetRevision: main # change this to "test"
    helm:
      parameters:
        - name: image.tag
          value: 1.16.0
      releaseName: child-app
```

3. Sync parent application with `Respect Ignore Differences` option
