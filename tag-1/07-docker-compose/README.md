# Docker Compose-Stack mit Wordpress und MariaDB aufsetzen

## Ziel

In dieser Übung werden wir einen Docker Compose-Stack erstellen, der aus zwei Services besteht: Wordpress und MariaDB. Wir werden auch die Konzepte von Volumes und Networks erläutern, um besser zu verstehen, wie diese Elemente in Docker Compose verwendet werden.

## Schritte

### Schritt 1: Erstellen einer `docker-compose.yml`-Datei

Erstellen wir zunächst eine neue Datei namens `docker-compose.yml` in einem neuen Projektverzeichnis. Der Inhalt der `docker-compose.yml`-Datei sollte wie folgt aussehen:

```yaml
version: "3.9"

services:
  db:
    image: mariadb:latest
    command: '--default-authentication-plugin=mysql_native_password'
    environment:
      MYSQL_ROOT_PASSWORD: my-secret-pw
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: my-secret-pw
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - wpnet

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: my-secret-pw
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8080:80"
    networks:
      - wpnet

networks:
  wpnet:
    driver: bridge

volumes:
  db_data:
  wordpress_data:
```

### Schritt 2: Verstehen der Konzepte von "Services", "Volumes" und "Networks"

**Services**: In einem Docker Compose-Stack definieren und konfigurieren wir Services, die die Container und ihre Einstellungen darstellen. In diesem Beispiel haben wir zwei Services: `db` und `wordpress`.

**Volumes**: Volumes sind persistente Speicherbereiche, die von einem oder mehreren Containern verwendet und geteilt werden können. In unserem Beispiel haben wir zwei Volumes, eines für die MariaDB-Daten (`db_data`) und eines für die Wordpress-Dateien (`wordpress_data`).

**Networks**: Networks ermöglichen die Kommunikation zwischen Containern. In unserem Beispiel haben wir ein einzelnes Netzwerk namens `wpnet`, das einen Bridge-Typ verwendet, damit die `wordpress` und `db` Services miteinander interagieren können.

### Schritt 3: Starten des Docker Compose-Stack

Navigieren wir im Terminal zu dem Verzeichnis, in dem sich die `docker-compose.yml`-Datei befindet, und führen den folgenden Befehl aus, um den Stack zu starten:

```sh
docker-compose up -d
```

Dadurch werden die Services gestartet und die Container erstellt. Lassen wir den Stack einige Zeit laufen, bis die Container vollständig initialisiert sind.

### Schritt 4: Zugriff auf die Wordpress Website

Nachdem der Stack gestartet und initialisiert wurde, öffnen wir einen Webbrowser und gehen zu `http://localhost:8080`, um auf die Wordpress-Installation zuzugreifen. Dort sollten wir das Wordpress-Setup sehen und dem Assistenten folgen können, um die Website zu erstellen.

### Schritt 5: Einrichtung einer MariaDB-Webschnittstelle (phpMyAdmin)

In diesem Schritt fügen wir phpMyAdmin zum Docker Compose-Stack hinzu, um eine Webschnittstelle für die Verwaltung der MariaDB-Datenbank bereitzustellen.

Aktualisieren wir zunächst die `docker-compose.yml`-Datei, um einen neuen Service namens `phpmyadmin` hinzuzufügen:

```yaml
version: "3.9"

services:
  db:
    image: mariadb:latest
    command: '--default-authentication-plugin=mysql_native_password'
    environment:
      MYSQL_ROOT_PASSWORD: my-secret-pw
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: my-secret-pw
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - wpnet

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: my-secret-pw
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8080:80"
    networks:
      - wpnet
  
  # Neu hinzugekommen
  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin:latest
    environment:
      PMA_HOST: db
      PMA_USER: wordpress
      PMA_PASSWORD: my-secret-pw
    ports:
      - "8081:80"
    networks:
      - wpnet
  # Ende: Neu hinzugekommen

networks:
  wpnet:
    driver: bridge

volumes:
  db_data:
  wordpress_data:
```

Diese Änderungen fügen einen neuen Service `phpmyadmin` hinzu, der auf das offizielle phpMyAdmin-Bild zugreift, es konfiguriert und auf Port 8081 verfügbar macht.

Navigieren wir im Terminal zu dem Verzeichnis, in dem sich die `docker-compose.yml`-Datei befindet, und führen den folgenden Befehl aus, um den Stack zu aktualisieren:

```sh
docker-compose up -d
```

Warten Sie, bis der Stack aktualisiert wurde und der `phpmyadmin` Container vollständig initialisiert ist.

Öffnen Sie Ihren Webbrowser und navigieren Sie zu `http://localhost:8081`, um auf die phpMyAdmin-Oberfläche zuzugreifen. Hier können Sie sich mit den Datenbank-Anmeldedaten (Benutzername: `wordpress`, Passwort: `my-secret-pw`) anmelden und Ihre MariaDB-Datenbank verwalten.

### Schritt 6: Herunterfahren des Docker Compose-Stack

Nachdem Sie Ihre Arbeit mit Wordpress und php

### Schritt 6: Herunterfahren des Docker Compose-Stack

Wenn wir den Stack nicht mehr benötigen, navigieren wir zurück zum Terminal und führen im Verzeichnis, in dem sich die `docker-compose.yml`-Datei befindet, den folgenden Befehl aus:

```sh
docker-compose down
```

Damit werden die laufenden Container entfernt und das Netzwerk aufgelöst. Beachte jedoch, dass die Volumes bestehen bleiben und erneut verwendet werden können, wenn wir den Stack später wieder starten sollten.

**Fazit**: In dieser Übung haben wir gelernt, wie wir einen Docker Compose-Stack für Wordpress und MariaDB einrichten können. Außerdem haben wir die Konzepte von Services, Volumes und Networks kennengelernt.