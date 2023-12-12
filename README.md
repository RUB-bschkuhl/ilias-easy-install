# Ilias LMS in Docker

1. [Docker installieren](#docker-installieren)
    1. [Windows](#windows-docker)
    2. [macOS](#macos-docker)
2. [Installation von ILIAS](#ilias)
3. [Anmeldung im ILIAS](#iliasuser)
4. [Anmeldung in DB Container](#dbuser)

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
Ein elleganteter Weg zur Installation ist mit <a href="http://brew.sh">Homebrew</a> und <a href="http://caskroom.io/">Homebrew Cask</a>.
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

## Step-by-Step Installation von ILIAS via Terminal/Console  <a name="ilias">

`docker compose up`

`docker cp postCreateCommand.sh ilias-frontend:/tmp/postCreateCommand.sh`

`docker cp postStartCommand.sh ilias-frontend:/tmp/postStartCommand.sh`

`docker cp php.ini ilias-frontend:/tmp/php.ini`

`docker exec -it ilias-frontend /bin/bash`

`echo 'ServerName localhost' >> /etc/apache2/apache2.conf `

`cd /tmp/`

`bash postCreateCommand.sh`

`bash postStartCommand.sh`

Zu erreichen unter: http://localhost:8080/ilias-8/

## Anmeldung im ILIAS <a name="iliasuser">
* Der default user nach einer Erst-Installation ist `root`, das zugehörige Passwort `homer`.

## Anmeldung im DB Container <a name="dbuser">
* Nach der Installation kann die DB mit dem user `root` und Passwort `mariadb` aufgerufen werden.
