# Unser erster Docker-Container
Um uns langsam an Docker heranzutasten, starten wir einen Container vom Python 3-Image und testen, ob Python auch wirklich funktioniert

```shell
docker run -it --rm python:3 python
```
Lass' dir nun den heutigen Tag ausgeben.
```python
from datetime import date
str(date.today())
# '2023-12-06'
```
Den Interpreter kannst du mit STRG+D verlassen – so wie auch den Container.