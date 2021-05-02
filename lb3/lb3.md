![Titelblatt_M300](images/M300_Titelblatt.png)

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




## Testen <a name="testen"></a>


## Quellenverzeichnis <a name="Quellen"></a>

