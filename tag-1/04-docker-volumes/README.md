# Bind-Mounts mit Docker

Lege auf dem Host eine Datei `script.py` an und fülle sie mit einem kleinen Python-Skript. Beispiel: `print("hello world")`.

Starte einen Container vom `python:3` Image mit bash als Kommando und mounte das Verzeichnis, in dem das Skript liegt, in `/tmp/scripts`
```shell
docker run -it --rm -v .:/tmp/scripts python:3 bash
```
Führe das Skript aus
```shell
python /tmp/scripts/script.py
```