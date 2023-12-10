# Docker Container

## Aufgabe 1

Erzeuge einen Container vom node:latest Image und nenne es "ser-node"

```shell
docker create --name ser-node node:latest
# bf3778e57ced6bce6cea91b56f8e6d8b34ba8d033312cc54b05d53d88857bb7e
```

Lass‘ dir den Container mit dem ls-Befehl anzeigen (an das -a Flag denken)
```shell
docker container ls -a
# CONTAINER ID   IMAGE       NAME      COMMAND                  CREATED          STATUS
# bf3778e57ced   node:latest ser-node "docker-entrypoint.s…"   49 seconds ago   Created 
```
Starte den Container
```shell
docker start ser-node
# ser-node
``` 
Stoppe den Container
```shell
docker stop ser-node
# ser-node
```

Lösche anschließend den Container

```shell
docker rm ser-node
# ser-node
```

## Aufgabe 2
Starte mit `docker run` einen Container vom `python:3` Image, allerdings mit der Bash als Standardprogramm.

```shell
$ docker run -it --rm python:3 bash
```

Starte `python` in diesem Container. 
Wenn du den Python-Interpreter mit STRG-D schließt, was passiert bzw. was passiert nicht?

## Aufgabe 3

Starte mit `docker create` und `start` einen nginx Container, aber verbinde dich noch nicht mit ihm.

```shell
docker create --name praxisaufgabe nginx
docker start praxisaufgabe
```
Führe die Befehle `apt-get update` und `apt-get install nano -y` auf dem Container aus.
```shell
docker exec praxisaufgabe "apt-get" "update"
docker exec praxisaufgabe "apt-get" "install" "nano" "-y"
```
Verbinde dich mit dem Container durch eine Bash-Sitzung und starte `nano`.
```shell
docker exec -it praxisaufgabe2 bash
```
