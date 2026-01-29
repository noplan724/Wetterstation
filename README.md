# Tiny Mac Wetterstation 🌤️💾

![MacTiny Screenshot](https://i.ibb.co/9mZ4Zf71/tinymac2.png)

Eine Retro-Wetterstation im Stil des klassischen Macintosh OS (System 6/7). Läuft auf einem Raspberry Pi (mit Hardware-PWM Support) oder jeden Linux-Server (Debian/Ubuntu/Proxmox). Dieses Tool wurde ursprünglich für den Tiny Mac mit Raspberry Pi Zero (2) (https://www.instructables.com/Making-a-Tiny-Mac-From-a-Raspberry-Pi-Zero/) entwickelt, funktioniert aber auch auf jedem anderen Gerät im Webbrowser. 

Die Station zeigt Wetterdaten von OpenWeatherMap und lokale Feinstaubwerte von Sensor.Community an.

## 📋 Funktionen

* **Retro Design:** Macintosh OS (System 6/7) Interface.
* **Multi-User fähig:** Konfiguration erfolgt über URL-Parameter.
* **Historie:** Speichert 24h Verlauf für jeden Sensor separat.
* **Server-Safe:** Läuft auch auf normalen Servern (LXC/Docker), Hardware-Funktionen werden dann ignoriert.
* **Nachtmodus:** Automatische Helligkeitsregelung (nur Raspberry Pi). Wenn die Software auf einem Raspberry Pi läuft und ein Display via PWM an **GPIO 18** angeschlossen ist (z.B. Waveshare DPI Displays), regelt die Station die Helligkeit automatisch anhand der Uhrzeit:
  * **Tagsüber (07:00 - 22:00 Uhr):** 100% Helligkeit.
  * **Nachts (22:00 - 07:00 Uhr):** 30% Helligkeit. Auf Systemen ohne den entsprechenden PWM-Chip (Proxmox, PC, Cloud) wird diese Funktion automatisch deaktiviert und ignoriert.

## 📂 Verzeichnisstruktur

Damit die App funktioniert, muss deine Ordnerstruktur exakt so aussehen:

```text
wetterstation/
├── app.py                 # Der Hauptserver (Python Code)
├── requirements.txt       # Liste der benötigten Pakete (Optional)
├── templates/
│   └── index.html         # Das Design (HTML/CSS/JS)
└── static/
    └── fonts/
        └── ChicagoFLF.ttf # WICHTIG: Schriftart hier ablegen!

```


## 🚀 Installation
1. Repository klonen & vorbereiten
Lade den Code auf deinen Server/Pi.

2. Schriftart besorgen
Aus rechtlichen Gründen ist die Schriftart nicht enthalten.

Lade ChicagoFLF hier herunter: 
```
https://www.1001freefonts.com/de/chicago.font
```
Entpacke die ZIP-Datei.

Erstelle den Ordner static/fonts/ in deinem Projekt.

Kopiere die Datei ChicagoFLF.ttf dort hinein.

3. Umgebung einrichten (Empfohlen)
Es wird empfohlen, eine virtuelle Umgebung zu nutzen:

```text
# In den Ordner wechseln
cd wetterstation

# Virtuelle Umgebung erstellen
python3 -m venv venv

# Aktivieren
source venv/bin/activate

# Pakete installieren
pip install flask requests
```

## ▶️ Starten

Starte den Server mit folgendem Befehl:

```text
python3 app.py
```

Der Server läuft nun standardmäßig auf Port 5000. (Wenn du die Konsole schließt, stoppt der Server. Für Dauerbetrieb nutze systemd oder screen.)

## 🖥️ Nutzung & URL Parameter
Die Wetterstation wird komplett über die URL konfiguriert. So kannst du den Link an Freunde weitergeben, damit diese ihren Ort und ihren API-Key nutzen können.

Aufbau der URL: http://DEINE-IP:5000/?owm=KEY&lat=LAT&lon=LON&sensor=ID

Die Parameter:

owm: Dein OpenWeatherMap API Key (Kostenlos auf openweathermap.org erstellen).

lat: Die Breitengrad-Koordinate deines Ortes (z.B. 52.52).

lon: Die Längengrad-Koordinate deines Ortes (z.B. 13.40).

sensor (Optional): Die ID eines Feinstaubsensors von maps.sensor.community (z.B. 12345).

Beispiel-Link:

Ersetze die Platzhalter durch deine echten Werte (Beispielort: Mitte von Deutschland):

http://192.168.178.50:5000/?owm=dein_langer_api_key&lat=50.0&lon=10.0&sensor=12345

## 🖥️ Browser & Kiosk Modus
Für die korrekte Darstellung wird Firefox dringend empfohlen. In Chrome oder Chromium kann es zu unscharfen Schriften oder Darstellungsfehlern kommen.

Firefox auf Raspberry Pi / Debian installieren:
```
sudo apt update
sudo apt install firefox-esr
```
Vollbild nutzen: Öffne die URL in Firefox und drücke F11, um in den Vollbildmodus zu wechseln und die Browserleisten auszublenden.


## ⚖️ Lizenz
Der Quellcode (Python/HTML) steht unter der MIT Lizenz. Die Schriftart "ChicagoFLF" unterliegt eigenen Lizenzbestimmungen und ist Eigentum des jeweiligen Urhebers.

