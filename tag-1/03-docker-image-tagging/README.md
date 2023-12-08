# Docker Image Tagging

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
Vergleiche jeweils die Ausgabe, die dir das CLI zurückgibt
