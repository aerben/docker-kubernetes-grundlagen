# ReplicaSet

Dieses Beispiel illustriert, welche Rolle ReplicaSets bei Kubernetes spielen. Die Ressource, die wir uns anschauen, ist in [manifest.yaml](manifest.yaml) definiert.

Führen die folgenden Schritte durch, um die Demo zu starten:

1. Erstelle das ReplicaSet:

```sh
kubectl apply -f manifest.yaml
```

2. Stelle sicher, dass alle Pods korrekt erstellt wurden:

```sh
kubectl get pods --selector=app=replicaset-demo
```

3. Lösche einen Pod

```sh
# kubectl delete pod <POD_NAME>
# oder für bash-Profis um den ersten Pod zu löschen:
kubectl get pods --selector=app=replicaset-demo \
  --no-headers -o custom-columns=":metadata.name" \
  | head -n1 \
  | xargs kubectl delete pod
```

4. Prüfe die Podliste erneut.

```sh
kubectl get pods --selector=app=replicaset-demo 
```

Das ReplicaSet sollte nun wieder einen dritten Pod angelegt haben.

# Aufräumen
```shell
kubectl delete replicaset.apps/replicaset-demo
```