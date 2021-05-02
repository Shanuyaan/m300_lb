![Titelblatt_M300](../images/Modul300_lb3.png)

## Inhaltsverzechnis
- [Inhaltsverzechnis](#inhaltsverzechnis)
- [Einleitung <a name="Einleitung"></a>](#einleitung-)
- [Service Anwendung <a name="Serive-an"></a>](#service-anwendung-)
- [Service Beschreibung <a name="Service-be"></a>](#service-beschreibung-)
- [Grafische Übersicht <a name="Grafik"></a>](#grafische-übersicht-)
- [Code Beschreibung <a name="Code"></a>](#code-beschreibung-)
- [Testen <a name="testen"></a>](#testen-)
- [Quellenverzeichnis <a name="Quellen"></a>](#quellenverzeichnis-)

## Einleitung <a name="Einleitung"></a>

Im Modul 300 haben wir das Thema "Plattformübergreifende Dienste im Netzwerk integrieren" behandelt. Dazu haben wir ein Projekt gestartet. Zu Beginn haben wir die benötigte Tools installiert und getestet. Für unser Projekt müssen wir mit einem Repository arbeiten, in diesem Falle haben wir GitHub benutzt.
Dazu haben wir Docker und Docker-compose installiert.

In meinem Projekt setzte ich, mit hilfe von docker-compose, einen Service auf. Nextcloud ist der Name von der Software. Da ich nicht den Service zum ersten mal höre musste ich vieles dazu nachlesen um herauszufinden, was der Service alles mit sich bringt.

## Service Anwendung <a name="Serive-an"></a>

Um den Service Nextcloud zu nutzen braucht man zuerst eine laufende Docker umgebung mit Docker-compose.

- In das Verzeichnis wo sich das docker-compose.yml befindet.
- `docker-compose up -d`
- Danach öffnet man einen Browser und gibt in der Suchleiste `http:\\Docker-IP:8080\`
 
## Service Beschreibung <a name="Service-be"></a>

Nextcloud ist eine kostenlose Open-Source-Cloud-Software, mit der seine Daten aif seinem eigenen Server verschlüsselt abspeichern kann. Nextcloud ist eine Alternative zu Cloud-Speicher wie Dropbox, Google Drive und OneDrive.
Man kann mit Nextcloud ganz einfach seine Daten zuhause untereinander sharen und zugreifen.

## Grafische Übersicht <a name="Grafik"></a>


## Code Beschreibung <a name="Code"></a>

Am Anfang der Datei werden die Version der Konfigurationsdatei und drei Platzhalter für das Volume definiert.

```code Anfang
version: '3'

volumes:
  nextcloud:
  db:

```

Als nächstes folgt die Definition der Dienste, aus denen der eigentliche Teil der Anwendung besteht

Hier wird mit dem Öffnungstag `services:` begonnen, gefolgt von den einzelnen Diensten.

Nextcloud braucht für den Betrieb eine Datenbank, in der sämtliche Metadaten gesichert werden. Für das nenne ich die Datenbank  `nextcloud-db`

```Serivces
 nextcloud-db:
    image: mariadb
    container_name: nextcloud-db
    restart: always
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=nextcoloud
      - MYSQL_PASSWORD=nextcloud
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
```

Es müssen lediglich die Umgebungsvariablen, speziell `MYSQL_ROOT_PASSWORD` und `MYSQL_PASSWORD` gesetzt werden

Der Nextcloud-Container selbst wird als Service nextcloud beschrieben.

```nextcloud
  nextcloud:
    image: nextcloud
    container_name: nextcloud
    restart: always
    ports:
      - 8080:80
    depends_on:
      - nextcloud-db
    volumes:
      - ./config:/var/www/html/config
      - /nextcloud-data:/var/www/html/data
      - ./apps:/var/www/html/apps
      - ./custom_apps:/var/www/html/custom_apps
```

Hier sind keine weiteren Umgebungsvariablen zu setzen.

Die einzelnen Tags innerhalb der Service-Definitionen haben folgende Bedeutung.


| Tag           | Funktion      |
| ------------- | ------------- |
| image         | Das Image, welches von der Registry runtergeladen wird |
| container_name     | Frindly-name für den Docker-Container |
| restart | Neustart-Policy, hier wird der Container immer neugestartet wenn er nicht mehr läuft |
| ports | Freigegebene Ports, damit der Container auch von außerhalb erreichbar ist, z.B. dem eigenen PC|
| depends_on | 	Abhängigkeit von einem anderen Service, hier beispielhaft der zuvor definierten Datenbank. Der Container startet nur, wenn der andere Container vorhanden ist und läuft|
| volumes | Definition der persistenten Datenspeicher |
| environment | Umgebungvariablen, wie z.B. Passwörter oder Namen|

## Testen <a name="testen"></a>


## Quellenverzeichnis <a name="Quellen"></a>

