# Meshtastic-Informations-System-MIS
### Ein auf BBS basierendes Informationssystem für das Mestastic Netzwerk

Das System basiert auf dem [TC²-BBS Meshtastic](https://github.com/TheCommsChannel/TC2-BBS-mesh) von [TheCommsChannel](https://github.com/TheCommsChannel)

### Many thanks to [TheCommsChannel](https://github.com/TheCommsChannel) and everyone else who worked hard to create this great project.

Im Grunde ist es nur eine Übersetzung ins Deutsche mit ein paar kleinen Änderungen. Derzeit hat die Übersetzung noch nicht begonnen.

### Ich übernehme keine Haftung für Schäden an Geräten oder Komponenten, die durch die Verwendung dieses Codes oder der Anleitung dazu entstehen. Ich weise darauf hin, dass die Anleitung ggf. unvollständig oder fehlerhaft sein könnte. Bitte beachten Sie die gesetzlichen Vorschriften in Ihrem Land zur Verwendung dieser Software. Zu Risiken und Nebenwirkungen fragen Sie Ihren Admin oder Händler!

### Vorraussetzung:
- Als Plattform wird ein [Raspberry Pi 3 Model B+](https://www.raspberrypi.com/products/raspberry-pi-3-model-b-plus/) verwendet.
- Als Betriebssystem wird [DietPi v9.8](https://dietpi.com/) verwendet.
- Python 3.x
- Meshtastic
- pypubsub

Die Installation von DietPi wird [auf der Seite von DietPi](https://dietpi.com/docs/install/) beschriben. Ich gehe hier nicht näher darauf ein. Ich verwende DietPi nur aus Bequemlichkeit. Das MIS sollte aber auch auf anderen Betriebssystemen lauffähig sein.

### Installation:

Zuerst installieren wir [Meshtastic](https://meshtastic.org/docs/software/python/cli/installation/)

```sh 
cd ~
apt-get -y update && apt-get upgrade
sudo apt-get -y install python3 python3-pip screen git
sudo apt install -y pipx && pipx install meshtastic
pipx ensurepath
```
Nach der Installation muss die SSH Verbindung beendet und wiederverbunden werden!

Meshtastic sollte jetzt schon verwendbar sein. Wenn ein Node z.B. per USB verbunden ist, sollte der folgende Befehl Informationen zum Node auslesen und anzeigen:

```sh 
meshtastic --info
```
Weiter geht es mit der Installation von MIS:

```sh
git clone https://github.com/Neppumuck/Meshtastic-Informations-System-MIS.git
cd Meshtastic-Informations-System-MIS
```

Wir erstellen ein Python virtual environment:
```sh
python3 -m venv venv
```
Damit virtual environment wird aktiviert:
```sh
source venv/bin/activate
```
Es fehlen noch ein paar Dinge:
```sh
pip install -r requirements.txt
```
Umbenennen der Konfiguationsdatei:
```sh
mv example_config.ini config.ini
```
Die Installation ist jetzt abgeschlossen.

### Konfiguration

Im ersten Schriit sollten wir heruasfinden, welche Schnittstelle verwendet wird. In meinem Fall USB.
Folgender Befehl könnte dabei hilfreich sein:
```sh
dmesg | grep tty
```
Wir suchen zum Beispiel:
```sh
/dev/ttyUSB0
/dev/ttyAMA0
```

Es mach Sinn sich zu überlegen ob Zugriffsregelungen eingeführt werden sollen. Falls das der Fall sein sollte, sollten die ID´s der Nodes bekannt sein. dieser erhält man mit folgendem Befehl:
```shAnführungszeichen
meshtastic --nodes
```
Unter DietPi müssen die ID´s immer in einzelnen Anführungszeichen ' stehen. Zum Beispiel: '!433b8a64'
Für die, die das Zeichen nicht auf der Tastatur finden:
```sh
''
```
Bearbeiten wir die "config.ini" z.B. mit nano oder nach belieben:
```sh
nano config.ini
```
Es muss mindestens das Interface festgelegt werden:
```sh
[interface]
type = serial
port = /dev/ttyAMA0
```
Auf die restlichen Einstellungen gehe ich hier nicht näher ein. Diese werden im Zuge der Übersetzung selbsterklärend sein. Es genügt jetzt die Datei zu speichern und den ersten Start durchzuführen:
```sh
python server.py
```
Wenn alles geklappt hat, sollte das MIS starten und von Meshtastic Nodes ansprechbar sein.

Tipp: Ich lasse den Server gerne mit [Screen](https://wiki.ubuntuusers.de/Screen/) im Hintergrund laufen.

### Autostart

Soll das MIS beim Start des Raspberry gestartet werden, muss folgedes umgesetzt werden:

Die Datei "mesh-bbs.service" muss bearbeitet werden:
```sh
User=root 
WorkingDirectory=/root/Meshtastic-Informations-System-MIS
ExecStart=/root/Meshtastic-Informations-System-MIS/venv/bin/python3 /root/Meshtastic-Informations-System-MIS/server.py
```
oder z.B.
```sh
User=pi
WorkingDirectory=/home/pi/Meshtastic-Informations-System-MIS
ExecStart=/home/pi/Meshtastic-Informations-System-MIS/venv/bin/python3 /home/pi/Meshtastic-Informations-System-MIS/server.py
```
Es folgt das einrichten des Dienstes:
```sh
sudo cp mesh-bbs.service /etc/systemd/system/
```
Autostart aktivieren:
```sh
sudo systemctl enable mesh-bbs.service
```
Autostart deaktivieren:
```sh
sudo systemctl disable mesh-bbs.service
```

Start sofort:
```sh
sudo systemctl start mesh-bbs.service
```
Stop:
```sh
sudo systemctl stop mesh-bbs.service
```
Status:
```sh
sudo systemctl status mesh-bbs.service
```
Neustart:
```sh
sudo systemctl restart mesh-bbs.service
```
Vergangenes Logbucheinträge anzeigen:
```sh
journalctl -u mesh-bbs.service
```
Live Logbuch:
```sh
journalctl -u mesh-bbs.service -f
```

## Anmerkungen:

Als Rollen für den Note funktionieren

- **Client**
- **Router_Client**

## Was kann das MIS?

- **Mail System**: Senden und Empfangen von Nachrichten an Nodes.
- **Bulletin Boards**: Eine Art Pinnwand für Informationen in form von Nachrichten.
- **Channel Directory**: Ein Verzeichniss für Meshtastic Kanäle.
- **Statistics**: Statistiken von Nodes, Hardware und Rollen.
- **Wall of Shame**: Zeigt Geräte mit niedrigem Akkustand.
- **Fortune Teller**: Zufällig generierte Wahrsage. Unnötig, aber kostet nichts.

Weitere Informationen und Codeschnipsel folgen in kürze. Primär folgt jetzt die Übersetzung.
