# Dockerfiles

In dieser Aufgabe legen wir eine kleine Flask-Anwendung an, verpacken sie in ein Docker-Image und starten einen Container davon.

Baue zuerst das Image mit den in diesem Verzeichnis gegebenen Dateien.
```shell
docker build -t my_flask_app .
```

Starte nun einen Container davon
```shell
docker run --rm -d -p 8080:80 --name my_flask_container my_flask_app
```

Öffne nun einen Browser auf http://localhost:8080 und schau, ob die Anwendung läuft.

Schau dir die Logs an
```shell
docker logs my_flask_container
```
Cleanup:
```shell
docker stop my_flask_container
docker container rm my_flask_container
docker image rm my_flask_app
```
