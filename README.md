# Meshtastic-Informations-System-MIS
### Ein auf BBS basierendes Informationssystem für das Mestastic Netzwerk

Das System basiert auf dem [TC²-BBS Meshtastic](https://github.com/TheCommsChannel/TC2-BBS-mesh) von [TheCommsChannel](https://github.com/TheCommsChannel)

### Many thanks to [TheCommsChannel](https://github.com/TheCommsChannel) and everyone else who worked hard to create this great project.

Im Grunde ist es nur eine Übersetzung ins Deutsche mit ein paar kleinen Änderungen.

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
Umbenennen der Konfgiuationsdatei:
```sh
mv example_config.ini config.ini
```






```sh
```

[]()
