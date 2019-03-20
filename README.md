# iRadio
Ein Softwarebaukasten für den Aufbau neuer Radios oder dem Umbau alter Radios zu einem Internetradio auf Raspberry Pi Basis.

## Unterstützte Rechner:

 Raspberry 1A(+), 1B(+), 2B, 3A+, 3B(+) direkt mit Raspbian OS oder jedes andere Linux-OS mit APT-Paketverwaltungssystem. 
  
## Steuerung des iRadio durch:

Programmumschaltung / Lauststärkeänderung mit (Micro-)Taster, Inkrementaldrehgeber, Drehimpulsgeber, Fernsteuerbar über HTML-Bedienoberfläche http://IP_des_Radios:8080 oder über TCP/IP Sockets. 

Die Steuerung wird als Daemon "gpiod" realisiert.

## Unterstützte Displays für Nutzerschnittstelle:

### direkt über Lowlevel-GPIO (eigener Displaydaemon "displayd"):

- I²C LCD Module 16x2 und 20x4
- SSD1306 OLEDs
- ST7735 Displays
- 8bit Parallel ILI9325   
- 8bit Parallel ILI9327   
- 8bit Parallel ILI9341   
- 8bit Parallel ILI9342   
- 8bit Parallel ILI9481   
- 8bit Parallel SPFD5408   
- 8bit Parallel S6D1121   
- 8bit Parallel R61505U   
- 16bit Parallel ILI9341
- PWM-Servo getriebene Analogskale zum Beispiel für Programmplatz und Lautstärke

### Highlevel über Framebuffer/X11 (Displaydaemon oder Skalensimulation)

- alle HDMI Displays (auch LVDS über zusätzlichen HDMI-Controller)
- Röhrenbildschirme über FBAS Ausgang des Raspberry (auch einige andere Kleinrechner mit FBAS Ausgang)
- ST7735
- HX8340
- HX8353
- HX8347
- MI0283QT
- BD663474
- ILI9320
- ILI9325
- ILI9340
- ILI9341
- ILI9481
- ILI9486
- SSD1306
- AGM1264K
- UC1701
- RA8875
- SSD1289
- SSD1331
- SSD1351
- S6D1121
- S6D02A1
- PCD8544
- TLS8204
- UPD161704

## Zusatzfunktion:

Bei Raspberrys mit integrierter Bluetooth-Konnektivität, kann das iRadio als Bluetooth-Funklautsprecher arbeiten. Medieninhalte können über Bluetooth direkt zum iRadio gestreamt werden. Die Wiedergabe des Internetradioprogramms wird bei Verbindungsaufnahme über Bluetooth automatisch pausiert.

# Installation:

In /home/pi wird das Repository geklont.

`cd /home/pi/`

`git clone https://github.com/BM45/iRadio`

Wird das Repository als zip-Datei heruntergeladen, dann wird das heruntergeladene zip-Archiv mit `unzip` in /home/pi entpackt.

Die Basisinstallation des iRadios erfolgt durch Aufruf von install.sh mit Root-Rechten. Zur Basisinstallation wird eine Internetverbindung benötigt, da noch weitere Programmpakete installiert werden müssen.

`cd /home/pi/iRadio`

`sudo ./install.sh`

Nach dem Durchlauf des Installers und anschließendem Reboot des Raspberry, ist die Basisinstallation des Internetradios abgeschlossen. Zu diesem Zeitpunkt wird bereits die erste Internetradiostation der inkludierten Standardsenderliste abgespielt. Die Programmumschaltung kann durch Taster gegen Masse an den Pins 11 (GPIO17) und 12 (GPIO18) erfolgen.

Die Änderung der Pinbelegung oder Erweiterung der Tastensteuerung kann durch editieren von /home/pi/iRadio/gpiod.c erfolgen. Die Änderungen werden durch folgende Befehle übernommen.

`cd /home/pi/iRadio`

`sudo ./install_Tastensteuerung.sh`

`sudo reboot`

Anstelle von Tastern, kann auch ein Drehimpulsgeber zur Programmumschaltung genutzt werden.

![rotary](https://www.radio-bastler.de/forum/attachment.php?thumbnail=56549)

Hierzu muss ein neuer Steuerdaemon (gpiod) gebaut werden. Dies geht automatisch durch folgende Befehle.


`cd /home/pi/iRadio`

`sudo ./install_Drehencoder.sh`

`sudo reboot`

Nach dem Reboot des Raspberry kann man die Internetradioprogramme durch einen Drehimpulsgeber an den Pins 11 (GPIO17) und 12 (GPIO18) umschalten.

Eine Änderung der Pinbelegung oder Erweiterung der Drehimpulssteuerung (zum Beispiel für die Verstellung der Lautstärke über einen zweiten Drehimpulsgeber) kann durch editieren von /home/pi/iRadio/rotary.c erreicht werden. Die Änderungen werden durch folgende Befehle übernommen.


`cd /home/pi/iRadio`

`sudo ./install_Drehencoder.sh`

`sudo reboot`

![myimage-alt-tag](https://www.radio-bastler.de/forum/attachment.php?thumbnail=56759)
