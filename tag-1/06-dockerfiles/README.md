# Dockerfiles

## Aufgabe 1

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

## Aufgabe 2

Diese Aufgabe ist freier als Aufgabe 1 und es gibt mehrere Möglichkeiten, sie zu lösen.

- Setze das `nginx`-Image ein, um einen Webserver-Container zu starten. 
- Dieser soll auf dem Host unter Port 9000 erreichbar sein. 
- Er soll eine HTML-Datei anzeigen, in deren Inhalt "Hello World" steht. 
- Die HTML-Datei soll bereits im Image vorhanden sein.

### Hinweise:

- NGINX lauscht im Container standardmäßig auf Port 80. Auf dem Host soll NGINX aber unter Port 9000 erreichbar sein. Dabei hilft dir das `-p` Argument.
- In NGINX liegen die HTML-Dateien, die ausgeliefert werden, unter `/usr/share/nginx/html/`
- Der Name der HTML-Datei, der zuerst ausgeliefert wird, ist `index.html`
- Du kannst für diese Aufgabe gerne die offizielle Doku googeln, ChatGPT benutzen oder mich fragen, wenn du Hilfe brauchst :) 

### Bonus 1 für die Schnellen unter euch:

- Entferne die index.html aus der Dockerfile
- Binde sie mittels Bind Mount ein
- Baue das Image neu und starte einen neuen Container vom neuen Image.
- Stelle sicher, dass unter Port 9000 wieder NGINX läuft und die index.html anzeigt.

### Bonus 2 für die ganz Schnellen:

- Benutze weder Dockerfile noch Bind Mount, sondern den `cp`-Befehl, um die index.html in den Container zu verschieben.

### Aufräumen

Ganz am Ende bitte per Docker CLI oder Docker Desktop alle Images und Container löschen.

Es per Docker CLI zu machen ist eine gute Übung! 

Mit `docker images` und `docker container ls -a` könnt ihr alle Images und Container finden und sie dann mit den Befehlen `docker image rm <IMAGE>` bzw. `docker rm <CONTAINER>` löschen. 