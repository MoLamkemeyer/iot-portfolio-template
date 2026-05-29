
## Reflection 3
[Reflection 3](/Reflections/ref03.md)

## Reflection 4
[Reflection 4](/Reflections/ref04.md)

## Modul 06

**Teamarbeit** 
mit [Frederik Bröckling](https://github.com/fbroeckling/Portfolio-of-Frederik-Br-ckling)
mit [Emil Memetov](https://github.com/emilmemetov02-max/iot-portfolio-Emil-Memetov/tree/main/Module06) . Die Dokumentation für die Aufgaben des Modul 06 sind ab der Aufgabe 2 hauptsächlich bei [Emil Memetov](https://github.com/emilmemetov02-max/iot-portfolio-Emil-Memetov/tree/main/Module06) und wurde zusammen erledigt.

## Aufgabe 1: Skalierung von IoT-Systemen

**1. Systembausteine & Schwachstellen (Pain Points) ohne Framework**

Beim manuellen Aufbau von IoT-Netzwerken (z. B. rein über die Arduino IDE oder isolierte PlatformIO-Projekte) stößt man bei der Systemvergrößerung unweigerlich an strukturelle und logistische Grenzen: 

•	Entwicklungs- & Flash-Overhead: Das serielle Kompilieren und physische Flashen über USB-Kabel ist im Klassenraum oder Labor extrem zeitaufwendig. Schlechte Kabel oder Treiberkonflikte führen zu einer hohen Fehlerquote. 

•	Management-Overhead: Die manuelle Pflege und Festlegung von Wi-Fi-Zugangsdaten, IP-Adressen, Passwörtern und MQTT-Broker-Zielen direkt im Quellcode skaliert nicht auf hunderte Geräte. Jede Netzwerkänderung erzwingt ein neues Flashen aller Knoten. 

•	Mangelndes Testing & Defektsuche: Ohne standardisierte Simulations- oder zentrale Logging-Umgebungen ist die Fehlersuche in einem verteilten, integrierten System kaum realisierbar. Unitlevel- und Integrationstests sind manuell hochgradig komplex. 

•	Mangelnde Dokumentation: Bei wachsender Geräteanzahl fehlt schnell die Übersicht über die exakte physische Pin-Belegung und die zugehörige MQTT-Topic-Struktur. 

**2. Anmerkungen zur Skalierung (Probleme & Anforderungen)**
Wenn die Anzahl der installierten Mikrocontroller massiv erhöht wird, verändern sich die Anforderungen an die Infrastruktur drastisch: 

•	Ressourcen- & Netzwerk-Overhead: Die verfügbare Bandbreite und die Verarbeitungskapazität des lokalen Netzwerks werden durch unfiltrierte Datenströme stark beansprucht. 

•	Mass Deployment (Massenbereitstellung): Sicherheitsupdates oder Logikänderungen müssen gleichzeitig auf eine Vielzahl von Geräten ausgerollt werden, ohne jedes Board einzeln per Kabel anzuschließen. 

•	Gewünschte Dienste für die Skalierung: Für den produktiven Betrieb größerer Systeme sind automatisierte Mechanismen zur Überwachung notwendig: 

o	Ein zentrales Logging-System zur Fehlerprotokollierung. 

o	Ein Knoten-Überwachungssystem (Node Monitoring) zur Live-Statuskontrolle. 

o	Simulations- und Stress-Testing-Umgebungen, um Systemgrenzen vor dem echten Deployment zu prüfen. 

**3. Gerätemanagement vs. Integration für IoT-Systeme**
Um große IoT-Systeme wartbar zu gestalten, muss die Architektur strikt in zwei funktionale Framework-Ebenen unterteilt werden: 

**A. Device-Management Frameworks (Geräteverwaltung)**

Diese Frameworks agieren direkt auf der Hardware-Ebene und verwalten den gesamten Lebenszyklus der Mikrocontroller (z. B. ESP8266 oder ESP32). 

•	Kernaufgaben: Automatische Firmware-Kompilierung, drahtlose Bereitstellung (Over-the-Air / OTA), physische Pin-Konfiguration und die automatische Anmeldung (Adoption) neuer Geräte im Netzwerk. 

•	Ziel: Aus der nackten Hardware einen einsatzbereiten, netzwerkfähigen IoT-Knoten (Node) zu generieren.

•	Wichtige Vertreter:

o	IoTempower: Maximal optimiert für die Lehre und schnelles Prototyping. Ermöglicht vollständig deklarative Konfigurationen über Verzeichnisstrukturen und ultrakurze setup.cpp-Dateien, bringt ein lokales Offline-Gateway mit und bietet einen sicheren, drahtlosen Adoption-Prozess. 

o	ESPHome: Konfiguration erfolgt komplett ohne C++ Kenntnisse über YAML-Dateien; nahtlose Integration in Home Assistant. 

o	Tasmota: Vorkompilierte Firmware für kommerzielle Smart-Home-Komponenten; Konfiguration erfolgt direkt über ein lokales Web-Interface. 

o	Mongoose OS: Professionelles, kommerzielles Open-Source-Betriebssystem mit Fokus auf JavaScript/C-Programmierung, TLS-Verschlüsselung und native Cloud-Anbindungen. 


**B. Integration Frameworks (System-Integration)**

Diese Frameworks arbeiten auf der Middleware- und Anwendungsebene. Sie setzen voraus, dass die Hardware bereits funktionsfähig im Netzwerk angemeldet ist. 

•	Kernaufgaben: Logische Verknüpfung und Orchestrierung der Datenströme zwischen den Geräten über Protokolle wie MQTT, Datenkonvertierung und Bereitstellung von grafischen Benutzeroberflächen (Dashboards). 

•	Ziel: Die herstellerunabhängige Kommunikation und die logische Verschaltung aller Komponenten zu einem funktionierenden Gesamtsystem.

•	Wichtige Vertreter:

o	Node-RED: Flussbasierte, visuelle Programmierung mit hoher Flexibilität durch eine riesige Auswahl an Community-Knoten und integrierter Dashboard-Erstellung. 

o	IoTknit: Python-basiertes Framework, das als leichtgewichtige, codebasierte Alternative zu Node-RED dient, um MQTT-Topics direkt via Skript zu orchestrieren. 

o	Home Assistant / OpenHAB: Führende Plattformen im Bereich der Heimautomatisierung mit umfassenden Datenbanken zur Integration kommerzieller Hardware. 

o	Apache NiFi / Flogo: Ausgelegt für industrielle Datenskalierung (Data Routing) und eventgesteuerte Mikro-Architekturen. 


## Task 2

Setting up iotempower

```
wsl --install

```
installing it and updating variables
```
curl -L https://now.iotempower.us | bash -
source ~/.bashrc
iot
```

Create the template and edit the system.conf file
```
cd ~/iot-systems
create_system_template my-home
cd my-home
nano system.conf
```
WiFi Settings
```conf
# Your WiFi network name
IOTEMPOWER_AP_NAME="MCU_ProgrammingFBML"

# Your WiFi password
IOTEMPOWER_AP_PASSWORD="HSBI2105"

# MQTT broker location
# If using OpenWRT router with mosquitto:
IOTEMPOWER_MQTT_HOST="192.168.1.1"

# If running mqtt_starter on your computer, use your computer's IP:
# Find it with: ipconfig (Windows) or ip a (Linux)
# IOTEMPOWER_MQTT_HOST="192.168.1.100"
# (replace with your actual IP - shown when mqtt_starter starts)
# Note: You may need to allow port 1883 in your firewall
```

Edit setup.cpp in node
```
cd ~/iot-systems/my-home
create_node_template living-room-lamp
cd living-room-lamp
nano setup.cpp
```

```cpp
// Button on pin D3
input(button1, D3, "released", "pressed").debounce(5);

// Onboard LED (note: inverted for most ESP boards)
output(blue_led, ONBOARDLED).inverted();
```

and then deploying after forwarding  the port via WSL USB  
<img width="728" height="854" alt="image" src="https://github.com/user-attachments/assets/f39a50c1-1f4d-4d77-9ce6-3a981d873909" />


```
deploy serial
```
```
living-room-lamp/sleep_mgr ready
living-room-lamp/button1 released
living-room-lamp/blue_led off
```
## Task 3
Now we add a new node with an input button  
We name said node "node2"  

```
iot menu
```
```
mv new-node node2
cd node2
nano setup.cpp
```
```cpp
input(b1, D5, "up", "down");
```
After forwarding the port via WSL USB  
<img width="727" height="847" alt="image" src="https://github.com/user-attachments/assets/446a9591-1533-40b5-b66a-e82289b6a4db" />

we deploy the specific usb so that the other microcontroller does not accidentally gets flashes as well.
```
ls /dev/ttyUSB*
```
```
/dev/ttyUSB1
```
Listening to MQTT from the parentdirectory in order to hear from both the first node (living-room-lamp) and (node2)  
```
cd..
mqtt_listen
```

```
living-room-lamp/blue_led on
living-room-lamp/sleep_mgr ready
living-room-lamp/button1 released
living-room-lamp/blue_led off
node2/sleep_mgr ready
node2/b1 up
living-room-lamp/blue_led off
living-room-lamp/sleep_mgr ready
living-room-lamp/button1 pressed
living-room-lamp/blue_led off
node2/sleep_mgr ready
node2/b1 down
```

After verifying this, we coded via node-red and verified with MQTT Explorer  

This command can be used to start Node-Red  
```
iot x web_starter
```
ip: http://localhost:40080/nodered  
user: admin  
password: iotempire  
<img width="1919" height="1079" alt="Screenshot 2026-05-28 175334" src="https://github.com/user-attachments/assets/706455c2-bce4-4238-a018-69bb3ea25588" />

<img width="1918" height="1078" alt="Screenshot 2026-05-28 174147" src="https://github.com/user-attachments/assets/7a27aa34-34a0-4c81-8e3c-1f11eab78a6e" />

## Aufgabe 4

**LED Grün/Rot**

 ```cpp
// Grüne LED an Pin D5 für "Zutritt gewährt / Welcome"
led(green_led, D5);

// Rote LED an Pin D6 für "Alarm / Kein Zutritt"
led(red_led, D6);
```

<img width="1536" height="2048" alt="8e09ba73-4e52-4159-849f-14eb33740154" src="https://github.com/user-attachments/assets/816bad59-eeaf-4da0-a6da-1c7117279cb0" /> 

<img width="1536" height="2048" alt="image" src="https://github.com/user-attachments/assets/96d75025-d10f-40f3-bc63-158402a0e477" />

**RFID**

Erstellt von Emil: 

**Buzzer**

Erstellt von Frederik:

**OLED DISPLAY**

Erstellt von Minguel:

**NODE-RED**

Nodered haben wir gemeinsam entwickelt. 

<img width="1075" height="643" alt="93b2b4fa-38e1-4a51-b0aa-59b72e0c23cd" src="https://github.com/user-attachments/assets/b99d7f96-d691-4eb5-9e3e-307849e6c02e" />


**Hardware Aufbau**

<img width="1536" height="2048" alt="8e09ba73-4e52-4159-849f-14eb33740154" src="https://github.com/user-attachments/assets/9dad3d92-3cf3-4d14-a162-8062e695b96c" />

<img width="1536" height="2048" alt="acff2a19-bae1-44ec-9021-35a60d8d0bed" src="https://github.com/user-attachments/assets/d079e87f-c290-4ba2-b173-4e3f142de034" />

<img width="1536" height="2048" alt="24821751-5dd9-4ff8-9401-3be31aa359de" src="https://github.com/user-attachments/assets/48f3aff0-0c4b-42d5-bd3a-542cf9439ea5" />

<img width="1536" height="2048" alt="54fa75ff-6b8d-46fc-8bfc-cc523287c014" src="https://github.com/user-attachments/assets/8327f79e-29fb-4917-9f86-0a1319f18195" />

<img width="1075" height="643" alt="93b2b4fa-38e1-4a51-b0aa-59b72e0c23cd" src="https://github.com/user-attachments/assets/948a5158-4df7-4cca-968f-9ee7bb10184e" />
<img width="1536" height="2048" alt="0c627494-0d06-410c-a67c-a1341296ea23" src="https://github.com/user-attachments/assets/e0d322f8-3dea-4554-82cf-5c7962d6a4cd" />
