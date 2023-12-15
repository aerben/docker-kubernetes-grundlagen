# 1. Docker Client
Manchmal verhält sich das Docker CLI nicht so, wie es soll. Es ist wichtig zu wissen, wie man sich Informationen über die lokale Docker-Installation beschaffen kann.
```shell
docker version
```
## Fragen
Ermittle mit docker info folgende Informationen über den Daemon:
- Verfügbare CPU
- Verfügbarer Memory
- Version
- OS

# 2. Docker Daemon

Wir können uns auch Informationen über den Daemon ausgeben lassen. Der Docker Client wird dazu eine Verbindung zum Host aufbauen – der in unserem Fall auf der gleichen Maschine läuft.

```shell
docker info
```

## Fragen
1) Ermittle die folgenden Informationen:
   - Welche Runtime verwendet der Daemon zum Start der Container?
   - Welche sind insgesamt verfügbar?
   - Beschreibe mit eigenen Worten, was diese Informationen über die Beziehung vom Docker Daemon zum Host aussagen. Welche Rolle spielt die Runtime?
2) Ermittle folgende Informationen über die Laufzeit des Hosts:
   - Welches OS hat der Host?
   - Wie viele CPUs stehen zur Verfügung? 
   - Wieviel Memory steht zur Verfügung?


# 3. Docker Registries

Zuerst werde ich euch einmal die Registry "Docker Hub" zeigen und wie man Images auf ihr sucht.

_Danach_

Gehe auf https://hub.docker.com/ und suche nach dem Image `node`.
## Fragen
- Wie viele bekannte Sicherheitslücken hat das Image mit dem Tag `latest`?
- Welches Base-Image wurde für dieses Image benutzt? (Tipp: Auf den Hash des obersten Layers dieses Images klicken)
- Würdest du insgesamt sagen, dass man dieses Image in Produktion einsetzen kann?
- Egal ob du auf die letzte Frage mit "ja" oder "nein" geantwortet hast: Welchen Tag von "node" könnte man besser nehmen?