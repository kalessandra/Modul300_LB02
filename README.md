# Dokumentation LB02 Modul 300 Kalasch

# Table of contents
1. [Installierte Applikationen](#applikationen)
   1. [GitHub Account](#subparagraph1)
2. [Containerisierung](#paragraph1)
3. [Virtualisierung](#paragraph2)
4. [Docker](#paragraph3)
   1. [Installationsanleitung](#subparagraph2)
   2. [Docker Befehle](#subparagraph3)
5. [Testing](#paragraph4)
6. [Umgebung](#paragraph5)
7. [Versionsverwaltung / Git](#paragraph6)
8. [Mark Down](#paragraph7)
9. [Systemsicherheit](#paragraph8)
10. [Vergleich Vorwissen](#paragraph9)  
11. [Refelxion](#paragraph10)   

## Installierte Applikationen <a name="applikationen"></a>
HyperV  <br>
Docker  <br>
Visualstudio-Code  <br>
Git-Client  <br>
SSH-Key für Client erstellt  <br>

### GitHub Account <a name="subparagraph1"></a>
Ein GitHub Account wurde erstellt.

## Containerisierung <a name="paragraph1"></a>
 


## Virtualisierung <a name="paragraph2"></a>


## Docker <a name="paragraph3"></a>
Docker ist eine Freie Software zur Isolierung von Anwendungen mit Containervirtualisierung. Docker vereinfacht die Bereitstellung von Anwendungen, weil sich Container, die alle nötigen Pakete enthalten, leicht als Dateien transportieren und installieren lassen. Container gewährleisten die Trennung und Verwaltung der auf einem Rechner genutzten Ressourcen. Das beinhaltet laut Aussage der Entwickler: Code, Laufzeitmodul, Systemwerkzeuge, Systembibliotheken – alles was auf einem Rechner installiert werden kann. 

### Installationsanleitung <a name="subparagraph2"></a>
**Docker-Compose.yml File:** <br>
version: '2' <br>
services: <br>
   db: <br>
     image: mysql:5.7 <br>
     volumes: <br>
       - db_data:/var/lib/mysql <br>
     restart: always <br>
     environment: <br>
       MYSQL_ROOT_PASSWORD:  <br>
       MYSQL_DATABASE: wordpress <br>
       MYSQL_USER: wordpress <br>
       MYSQL_PASSWORD: wordpress <br>

   wordpress: <br>
     depends_on: <br>
       - db <br>
     image: wordpress:latest <br>
     ports: <br>
       - "8000:80" <br>
     restart: always <br>
     environment: <br>
       WORDPRESS_DB_HOST: db:3306 <br>
       WORDPRESS_DB_USER: wordpress <br>
       WORDPRESS_DB_PASSWORD: wordpress <br>
volumes: <br>
    db_data: <br>

**Befehl im CMD:** <br>
docker-compose up

**Webpage:** <br>
http://127.0.0.1:8000

### Docker Befehle <a name="subparagraph3"></a>

| Befehle | Beschreibung
| ------- | -----------
| docker run | Befehl zum Starten neuer Container
| docker ps | Überblick über die aktuellen Container, wie z.B. Namen, IDs und Status
| docker images | Liste lokaler Images aus, wobei Informationen zu Repository-Namen, Tag-Namen und Grösse enthalten sind
| docker rm | Entfernt einen oder mehrere Container. Gibt die Namen oder IDs erfolgreich gelöschter Container zurück
| docker rmi | Löscht das oder die angegebenen Images. Diese werden durch ihre ID oder Repository- und Tag-Namen spezifiziert
| docker start | Startet einen (oder mehrere) gestoppte Container
| docker stop | Stoppt einen oder mehrere Container (ohne sie zu entfernen). Nach dem Aufruf von docker stop für einen Container wird er in den Status »exited« überführt.
|  docker kill  | Schickt ein Signal an den Hauptprozess (PID 1) in einem Container. Standardmässig wird SIGKILL gesendet, womit der Container sofort stoppt.
| docker logs | Gibt die "Logs" für einen Container aus. Dabei handelt es sich einfach um alles, was innerhalb des Containers nach STDERR oder STDOUT geschrieben wurde.
| docker inspect | Gibt umfangreiche Informationen zu Containern oder Images aus. Dazu gehören die meisten Konfigurationsoptionen und Netzwerkeinstellungen sowie Volumes-Mappings.
| docker diff | Gibt die Änderungen am Dateisystem des Containers verglichen mit dem Image aus, aus dem er gestartet wurde.
| docker top | Gibt Informationen zu den laufenden Prozessen in einem angegebenen Container aus.
| docker build | Der Befehl docker build erfordert ein Dockerfile und einen Build Context. 

#### Dockerfile Anweisungen <a name="subparagraph2"></a>

| Befehle | Beschreibung 
| ------- | -----------
| ADD | Kopiert Dateien aus dem Build Context oder von URLs in das Image
| CMD | Führt die angegebene Anweisung aus, wenn der Container gestartet wurde. Ist auch ein ENTRYPOINT definiert, wird die Anweisung als Argument für ENTRYPOINT verwendet. 
| COPY | Wird verwendet, um Dateien aus dem Build Context in das Image zu kopieren. Es gibt die zwei Formen COPY src dest und COPY ["src", "dest"]. Das JSON-Array-Format ist notwendig, wenn die Pfade Leerzeichen enthalten.
| ENTRYPOINT | Legt eine ausführbare Datei (und Standardargumente) fest, die beim Start des Containers laufen soll.Jegliche CMD-Anweisungen oder an docker run nach dem Imagenamen übergebenen Argumente werden als Parameter an das Executable durchgereicht.ENTRYPOINT-Anweisungen werden häufig genutzt, um "Start-Scripts" anzustossen, die Variablen und Services initialisieren, bevor andere übergebene Argumente ausgewertet werden.
| ENV | Setzt Umgebungsvariablen im Image.
| EXPOSE | Erklärt Docker, dass der Container einen Prozess enthält, der an dem oder den angegebenen Port(s) lauscht
| HEALTHCHECK | Die Docker Engine prüft regelmässig den Status der Anwendung im Container.
| MAINTAINER | Setzt die "Autor-Metadaten" des Image auf den angegebenen Wert.
| RUN | Führt die angegebene Anweisung im Container aus und bestätigt das Ergebnis.
| SHELL | Die Anweisung SHELL erlaubt es seit Docker 1.12, die Shell für den folgenden RUN-Befehl zu setzten. So ist es möglich, dass nun auch direkt bash, zsh oder Powershell-Befehle in einem Dockerfile genutzt werden können.
| USER | Setzt den Benutzer (über Name oder UID), der in folgenden RUN-, CMD- oder ENTRYPOINT-Anweisungen genutzt werden soll.
| VOLUME | Deklariert die angegebene Datei oder das Verzeichnis als Volume. Besteht die Datei oder das Verzeichnis schon im Image, wird sie bzw. es in das Volume kopiert, wenn der Container gestartet wird.
| WORKDIR | Setzt das Arbeitsverzeichnis für alle folgenden RUN-, CMD-, ENTRYPOINT-, ADD oder COPY-Anweisungen.


## Testing <a name="paragraph4"></a>
| Testfall | Funktioniert / Nicht Funktioniert
| ------- | -----------
| Zugriff auf 127.0.0.1:8000 funktioniert | Es hat funktioniert
| Beitäge auf der Seite erstellen | Die Beiträge sind auf http://127.0.0.1:8000/?p=5 sichtbar
| Über mich Seite erstellt | Seite ist auf http://127.0.0.1:8000/?page_id=7 sichtbar

## Umgebung <a name="paragraph5"></a>
|Web-Server|
| -------- |
| IP Addresse : 127.0.0.1|
|Port: 8000|
|Volume: /var/ww/html|
+---------------------------+  
! Web-Server                ! 
!                           !  
! IP  Adresse: 127.0.0.1    ! 
! Port: 8000                !      
! Volume: /var/www/html     !       
+---------------------------+
 



## Versionsverwaltung / Git <a name="paragraph6"></a>


## Mark Down <a name="paragraph7"></a>


## Systemsicherheit <a name="paragraph8"></a>


## Vergleich Vorwissen <a name="paragraph9"></a>



## Reflexion <a name="paragraph10"></a>

