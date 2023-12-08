# Deployments und Rolling Updates

Das [Manifest](manifest.yaml) enthält ein Deployment mit einem einfachen NGINX-Container, für den drei Replika-Pods angelegt werden.
An diesem Manifest kann man folgende Eigenschaften erkennen.


- `apiVersion: apps/v1`: gibt an, dass wir die Deployment API von Kubernetes verwenden.
- Deployment mit dem Metadaten-Namen `deployment-demo`.
- `replicas: 3`: gibt an, dass 3 Replikate der Anwendung erstellt werden sollen.
- `strategy.type: RollingUpdate`: bestimmt die Aktualisierungsstrategie als RollingUpdate.
- `rollingUpdate.maxSurge: 1`: gibt an, wie viele Replikate während der Aktualisierung zusätzlich zur gewünschten Anzahl an Replikaten erstellt werden dürfen.
- `rollingUpdate.maxUnavailable: 0`: legt fest, wie viele Replikate während der Aktualisierung nicht verfügbar sein dürfen.
- `selector.matchLabels.app: rollingupdate`: zum Erkennen der App mit dem Label `rollingupdate`.
- Die Container nutzen das Image `nginx:alpine3.17` und lauschen auf Port `80`.

## Beispiel ausführen

1. Erstelle das Deployment.

```bash
kubectl apply -f manifest.yaml
```

2. Überprüfe den Status des Deployments:

```bash
kubectl rollout status deployment/deployment-demo
```

```shell
kubectl get pod --selector=app=deployment-demo
```

3. Führe ein Rolling-Update auf eine neue Imageversion durch, z.B. `nginx:alpine3.18`:

```bash
kubectl set image deployment/deployment-demo nginx=nginx:alpine3.18
```

4. Überwache das Rolling-Update:

```bash
kubectl rollout status deployment/deployment-demo
```

5. Falls du das Rolling-Update rückgängig machen musst:

```bash
kubectl rollout undo deployment/deployment-demo
```

6. Um den Verlauf des Deployments anzeigen lassen:

```bash
kubectl rollout history deployment/deployment-demo
```

# Aufräumen
```shell
kubectl delete deployment.apps/deployment-demo
```