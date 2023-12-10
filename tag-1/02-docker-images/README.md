# 1:  Docker Images

Um uns näher mit dem Docker CLI vertraut zu machen, schauen wir uns die lokal heruntergeladenen Images an.

```shell
docker images
```

```shell
docker inspect python:3
```
Diese Ausgabe ist sehr umfangreich und wegen des JSON-Formats nicht leicht zu lesen.
Mit dem `--format` Argument können wir mithilfe der Go-Template-Sprache auch einzelne Elemente der Image-Beschreibung ermitteln. 

```shell
docker inspect python:3 --format "{{.RootFS}}"
```

### Fragen ###  
- Ermittle das OS des Images `python:3`. Das Feld heißt im JSON `.Os`.
- Wann wurde es angelegt? (Das Feld heißt `.Created`)
- Welche Umgebungsvariablen sind definiert? (`.Config.Env`)


# 2: Docker Image Tagging

Finde über DockerHub das offizielle node-Image und pulle das image mit dem latest-Tag

```shell
docker pull node:latest
```

Tagge dieses image danach mit dem tag „my-node“

```shell
docker image tag node:latest my-node
```

Zeige dir mit docker inspect alle Tags an, die das Image „node“ bei dir lokal hat

```shell
docker image inspect node:latest --format "{{ .RepoTags }}"
```

Lösche nun zuerst dein Tag „my-node“ und danach das node-Latest-Image
```shell
docker image rm my-node
docker image rm node:latest
```
## Fragen
- Vergleiche jeweils die Ausgabe, die dir das CLI in den beiden letzten Kommandos oben zurückgibt
- Aus welchen Komponenten besteht ein Docker Tag?
- Beschreibe mit eigenen Worten, was ein Docker-Tag ist.
