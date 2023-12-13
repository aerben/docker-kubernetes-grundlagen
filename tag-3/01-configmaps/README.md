# Arbeiten mit ConfigMaps

## Übung 1: Erstellen einer ConfigMap

Wir erstellen eine ConfigMap mit dem Namen my-config, die zwei Schlüssel-Wert-Paare enthält: `key1: value1` und `key2: value2`.

Wir werden sowohl imperative als auch deklarative Methoden verwenden, um die ConfigMap zu erstellen.

#### Imperative Methode

```bash
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

Um die ConfigMap wieder zu löschen:

```shell
kubectl delete configmap my-config
```

#### Deklarative Methode

Siehe die Datei [declarative-config.yaml](). Wir können sie direkt mit kubectl anwenden. Danach lassen wir uns den Inhalt direkt ausgeben.

```bash
kubectl apply -f declarative-config.yaml
kubectl get configmap my-config -o "jsonpath= {.data.key1}"
```
Um die ConfigMap wieder zu löschen:

```bash
kubectl delete configmap my-config
```

## Übung 2: Importieren von Datei-Inhalten in eine ConfigMap

```bash
kubectl create configmap txt-config --from-file=sample.txt
kubectl describe configmap txt-config
```

Und um aufzuräumen:
```shell
kubectl delete configmap txt-config
```

## Übung 3: Verwenden einer ConfigMap in einem Pod

Die Datei [config-pod.yaml]() enthält die Deklarationen einer ConfigMap sowie einen Pod. Dieser loggt das `env` aus und stoppt danach. Wir können das Ergebnis in den Logs sehen.

```bash
kubectl apply -f config-pod.yaml
```

Überprüfen der Container-Logs:

```bash
kubectl logs config-pod
```
 
Aufräumen:

```bash
kubectl delete configmap my-config
```


## Übung 4: Aktualisieren einer ConfigMap

Bearbeiten einer ConfigMap:


```shell
kubectl apply -f declarative-config.yaml
kubectl get configmap my-config -o "jsonpath= {.data.key1}"
```
```bash
kubectl edit configmap my-config
```

Fügen wir die Zeile `key3: baz` unter "data" hinzu und speichern die Änderungen.
Ergebnis:

```shell
kubectl get configmap my-config -o "jsonpath= {.data.key3}"
```

Aufräumen:

```shell
kubectl delete configmap my-config
```

## Übung 5: Mappen von ConfigMap-Werten auf Volumen

Die Datei [volume-pod.yaml]() enthält eine ConfigMap, die per Volume in einen Pod gemountet wird. Wie im vorletzten Beispiel wird das Ergebnis geloggt, aber der Container wartet einige Zeit, bis er stoppt. Wir können ihn also mit exec untersuchen.

Anwenden der Datei:

```bash
kubectl apply -f volume-pod.yaml
```

Überprüfen der gemounteten Daten im Pod:

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
