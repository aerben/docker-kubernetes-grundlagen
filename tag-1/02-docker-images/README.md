# Docker Images

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

## Aufgaben ##  
- Ermittle das OS des Images `python:3`. Das Feld heißt im JSON `.Os`.
- Wann wurde es angelegt? (Das Feld heißt `.Created`)
- Welche Umgebungsvariablen sind definiert? (`.Config.Env`)