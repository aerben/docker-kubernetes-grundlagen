# NGINX StatefulSet mit Headless Service

Das [Manifest](manifest.yaml) erzeugt ein `StatefulSet` mit drei Replikas eines `nginx`-Pods, der den Container-Port 80 belegt. Außerdem wird ein `Service` definiert, der im sogenannten Headless-Modus läuft. Das bedeutet, dass er keine ClusterIP erhält (`clusterIP: None`). Wir schauen uns nun an, was genau dies bedeutet.

## Manifest anwenden
Zuerst legen wir die benötigten Ressourcen an und prüfen, ob sie korrekt erzeugt wurden.
```shell
kubectl apply -f manifest.yaml
```
```shell
kubectl get service nginx-headless
```
```shell
kubectl get pod --selector=app=nginx
```
## DNS untersuchen mit busybox

Wir verwenden `kubectl debug`, um einen Hilfscontainer zu starten. Wir untersuchen den ersten Pod des StatefulSet `nginx-0` und benutzen [busybox](https://github.com/mirror/busybox), ein Image zum Debuggen von Netzwerkproblemen.

Der DNS-Name des Services, den wir angelegt haben, ist 
`nginx-headless.default.svc.cluster.local` und wir werden sehen, dass dieser auf drei IP-Adressen verweist: eine pro Pod. Der Service selbst hat _keine_ ClusterIP! Nur die Pods haben eine IP, wie sie es immer haben (zumindest fast...).

Bei StatefulSet sind die Pods darüber hinaus über ihren Pod-Namen verfügbar:

```
<PODNAME>.<SERVICENAME>.<NAMESPACE>.svc.cluster.local
```
also z.B.
```
nginx-0.nginx-headless.default.svc.cluster.local
```
--- 
Viel Spaß beim Ausprobieren :) 

```shell
kubectl debug nginx-0 -it --image=busybox
```
```shell
nslookup nginx-headless.default.svc.cluster.local
```
```shell
nslookup nginx-0.nginx-headless.default.svc.cluster.local
```
## Aufräumen
```shell
kubectl delete statefulset.apps/nginx
kubectl delete service/nginx-headless
```