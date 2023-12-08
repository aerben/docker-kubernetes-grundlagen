# NGINX Pods und Services des Typs ClusterIP

Das [Manifest](manifest.yaml) erzeugt zwei Pods und einen Service. Da kein Type angegeben ist, fällt er auf den Default zurück: ClusterIP.

## Manifest anwenden
Zuerst legen wir die benötigten Ressourcen an und prüfen, ob sie korrekt erzeugt wurden.
```shell
kubectl apply -f manifest.yaml
```
```shell
kubectl get pod --selector=app=nginx-pod-demo
```

## DNS untersuchen mit busybox

Wir verwenden `kubectl debug`, um einen Hilfscontainer zu starten. Wir untersuchen den ersten Pod des StatefulSet `nginx-0` und benutzen [busybox](https://github.com/mirror/busybox), ein Image zum Debuggen von Netzwerkproblemen.

Der DNS-Name des Services, den wir angelegt haben, ist
`nginx-pod-demo-svc.default.svc.cluster.local` und wir werden sehen, dass dieser auf eine IP zeigt: die ClusterIP.

Über diese IP können wir den Nginx auf einem der beiden Pods erreichen.

```shell
kubectl debug nginx-pod-1 -it --image=busybox
```
```shell
nslookup nginx-pod-demo-svc.default.svc.cluster.local
wget -q -O- <IP>
```

## Aufräumen
```shell
kubectl delete service/nginx-pod-demo-svc
kubectl delete pod/nginx-pod-1
kubectl delete pod/nginx-pod-2
```

