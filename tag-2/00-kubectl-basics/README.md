# Kubectl basics

Um warm zu werden, testen wir lokal ob kubectl korrekt installiert ist.

```shell
kubectl get pods --all-namespaces # gibt alle Pods über alle Namespaces aus
```
```shell
kubectl get nodes # gibt alle aktiven Nodes aus. Bei minikube etwas langweilig :P
```
```shell
kubectl describe node minikube # Beschreibt den einzigen aktiven Node
```

Beantworte folgende Fragen:
- Wie viele CPUs stehen auf dem Node zur Verfügung?
- Welches Betriebssystem in welcher Version ist installiert?
- Wie viel Prozent des verfügbaren RAMs im Cluster sind genutzt? (Stichwort: "Allocated resources")
