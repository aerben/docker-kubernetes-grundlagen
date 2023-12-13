# Arbeiten mit ConfigMaps

## Übung 1: Erstellen einer ConfigMap

Wir erstellen eine ConfigMap mit dem Namen my-config, die zwei Schlüssel-Wert-Paare enthält: `key1: value1` und `key2: value2`.

Wir werden sowohl imperative als auch deklarative Methoden verwenden, um die ConfigMap zu erstellen.

#### Imperative Methode

Der folgende Befehl legt eine ConfigMap mit Namen "my-config" an und zwei Schlüssel-Wert-Kombinationen.
```bash
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

Lasst euch nun den Inhalt der neuen ConfigMap ausgeben:

```shell
kubectl get configmap my-config -o "jsonpath= {.data.key1}"
```

`jsonpath` dient dabei dazu, den Wert des Schlüssels `key1` direkt herauszusuchen und auszugeben.

Um anschließend die ConfigMap wieder zu löschen:

```shell
kubectl delete configmap my-config
```

#### Deklarative Methode

Die Datei [declarative-config.yaml]() enthält die gleiche ConfigMap, die wir oben angelegt haben, als YAML. Wir können sie direkt mit kubectl anwenden.

```bash
kubectl apply -f declarative-config.yaml
```

Lasst euch nun den Inhalt der neuen ConfigMap ausgeben:

```shell
kubectl get configmap my-config -o "jsonpath= {.data.key1}"
```

Um die ConfigMap wieder zu löschen:

```bash
kubectl delete configmap my-config
```

## Übung 2: Verwenden einer ConfigMap in einem Pod

Die Datei [config-pod.yaml]() enthält die Deklarationen einer ConfigMap sowie einen Pod. Dieser loggt das `env` aus und stoppt danach. Wir können das Ergebnis in den Logs sehen.

```bash
kubectl apply -f config-pod.yaml
```

Überprüfen der Container-Logs:

```bash
kubectl logs config-pod
```
In den Logs seht ihr alle Umgebungsvariablen, die der Pod kennt. Unter anderem sollten auch `key1` und `key2` enthalten sein. 

Aufräumen:

```bash
kubectl delete configmap my-config
```

## Übung 3: Mappen von ConfigMap-Werten auf Volumen

Die Datei [volume-pod.yaml]() enthält eine ConfigMap, die per Volume in einen Pod gemountet wird. Wie im vorletzten Beispiel wird das Ergebnis geloggt, aber der Container wartet einige Zeit, bis er stoppt. Wir können ihn also mit exec untersuchen.

Anwenden der Datei:

```bash
kubectl apply -f volume-pod.yaml
```

Wir prüfen nun, ob die Dateien erfolgreich in den Pod gemountet wurden:

```bash
kubectl exec -it volume-pod -- ls /etc/config 
```
```bash
kubectl exec -it volume-pod -- cat /etc/config/key1
```

Aufräumen:
```shell
kubectl delete configmap/my-config
kubectl delete pod/volume-pod
```
