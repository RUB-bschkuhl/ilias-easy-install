# Ilias LMS in Docker

0. [Sinn und Zweck](#sinn)
1. [Docker installieren](#docker-installieren)
    1. [Windows](#windows-docker)
    2. [macOS](#macos-docker)
2. [Installation von ILIAS](#ilias)
3. [Anmeldung im ILIAS](#iliasuser)
4. [Anmeldung in DB Container](#dbuser)

## Sinn und Zweck <a name="sinn"></a>
Dieses Repository dient als Basis für eine lokale ILIAS Installation die zu Testzwecken genutzt werden kann. Zugriff auf das Backend ist über die Verwendung von Docker möglich.
Mit der Installation ist eine vollständige Nutzung von ILIAS mit Admin-Priviligien möglich.
Zum aktuellen Zeitpunkt wird mit der Installation ILIAS 8 ausgeführt, eine Anpassung auf neuere und ältere Versionen von ILIAS kann in Kombination mit den Installationsfiles erfolgen.

Zu Entwicklungszwecken empfiehlt sich die Nutzung des folgenden Repositories welches für lokale Entwicklugnszwecke konzipiert ist:
https://github.com/MoodleNRW/ilias-vscode-dev-container

Folgende Schitte sind bei der Installation zu befolgen:

## Docker installieren <a name="docker-installieren"></a>

### Windows <a name="windows-docker">
#### 1. Docker Desktop für Windows installieren
https://www.docker.com/
* Beim Installieren darauf achten, dass das Häkchen ✔️ bei *Use WSL 2 instead of Hyper-V (recommended)* gesetzt ist.
* Anschließend Docker starten. Sobald das Rechteck unten links grün wird (beim Darüberfahren mit der Maus erscheint der Tooltip *Engine running*),
kann das Fenster geschlossen werden ❌
* ❗ Wichtig: Docker sollte weiterhin im Systemtray laufen (unten rechts in der Taskbar) ❗

### macOS <a name="macos-docker">
#### Variante 1: Docker Desktop für Mac mit brew installieren
Ein eleganteter Weg zur Installation ist mit <a href="http://brew.sh">Homebrew</a> und <a href="http://caskroom.io/">Homebrew Cask</a> möglich.
```bash
brew install --cask docker     # Installiert Docker
open /Applications/Docker.app  # Startet Docker
```
#### Variante 2: Docker Desktop über Download installieren
https://www.docker.com/
* Beim Download darauf achten, dass die richtige Chip-Variante ausgewählt wird (Intel Chip amd-64 vs Apple Chip arm-64).
* Herrausfindbar ist dies über das Apple-Menü () -> "Über diesen Mac" -> Chip / Prozessor Bezeichnung.
* Anschließend Docker starten. Sobald das Rechteck unten links grün wird (beim Darüberfahren mit der Maus erscheint der Tooltip *Engine running*),
kann das Fenster geschlossen werden ❌
* ❗ Wichtig: Docker sollte weiterhin laufen und der Prozess sollte nicht manuell beendet werden ❗
    
#### Empfehlung macOS
Um die Performance von Docker unter macOS maßgeblich zu verbessern sollte der VirtioFS Treiber aktiviert sein. Dieser findet sich in Docker Desktop unter *Settings -> Beta features -> Enable VirtioFS accelerated directory sharing*.

## Step-by-Step Installation von ILIAS via Terminal/Console im Projektordner <a name="ilias">

Im nächsten Schritt geht es um die tatsächliche Installation von ILIAS mittels dieses Repos. Hierzu wird zunächst der Quellcode lokal auf der ausführenden Maschine benötigt.
Der Code kann dazu, auch ohne git, als Zip heruntergeladen werden. Oben rechts im Profil der Button "<> Code" -> Download ZIP.
Nach dem entpacken der ZIP muss ein Terminal gestartet und in den Ordner navigiert werden.
Danach sind die Befehle in der folgenden Reihenfolge auszuführen.

`docker compose up -d`

`docker cp postCreateCommand.sh ilias-frontend:/tmp/postCreateCommand.sh`

`docker cp postStartCommand.sh ilias-frontend:/tmp/postStartCommand.sh`

`docker cp php.ini ilias-frontend:/tmp/php.ini`

`docker exec -it ilias-frontend /bin/bash`

`echo 'ServerName localhost' >> /etc/apache2/apache2.conf `

`cd /tmp/`

`bash postCreateCommand.sh`

`bash postStartCommand.sh`

Zu erreichen ist das lokale ILIAS LMS dann unter: http://localhost:8080/ilias-8/

Nachde die Befehle erfolgreich ausgeführt wurden ist die Docker Umgebung vollständig eingreichtet. Der Container kann dann entweder in der Docker Desktop Oberfläche oder über die Befehle im Projektordner gestartet oder gestoppt werden:

Start: `docker compose up -d`
Stop: `docker compose down`

## Anmeldung im ILIAS <a name="iliasuser">
* Der default user nach einer Erst-Installation ist `root`, das zugehörige Passwort `homer`.

## Anmeldung im DB Container <a name="dbuser">
* Nach der Installation kann die DB mit dem user `root` und Passwort `mariadb` im Docker terminal des db-containers aufgerufen werden.
