
## Reflection 3
[Reflection 3](/Reflections/ref03.md)


## Modul 06

## Aufgabe 1: Skalierung von IoT-Systemen

1. Systembausteine & Schwachstellen (Pain Points) ohne Framework

Beim manuellen Aufbau von IoT-Netzwerken (z. B. rein über die Arduino IDE oder isolierte PlatformIO-Projekte) stößt man bei der Systemvergrößerung unweigerlich an strukturelle und logistische Grenzen: 

•	Entwicklungs- & Flash-Overhead: Das serielle Kompilieren und physische Flashen über USB-Kabel ist im Klassenraum oder Labor extrem zeitaufwendig. Schlechte Kabel oder Treiberkonflikte führen zu einer hohen Fehlerquote. 

•	Management-Overhead: Die manuelle Pflege und Festlegung von Wi-Fi-Zugangsdaten, IP-Adressen, Passwörtern und MQTT-Broker-Zielen direkt im Quellcode skaliert nicht auf hunderte Geräte. Jede Netzwerkänderung erzwingt ein neues Flashen aller Knoten. 

•	Mangelndes Testing & Defektsuche: Ohne standardisierte Simulations- oder zentrale Logging-Umgebungen ist die Fehlersuche in einem verteilten, integrierten System kaum realisierbar. Unitlevel- und Integrationstests sind manuell hochgradig komplex. 

•	Mangelnde Dokumentation: Bei wachsender Geräteanzahl fehlt schnell die Übersicht über die exakte physische Pin-Belegung und die zugehörige MQTT-Topic-Struktur. 

2. Anmerkungen zur Skalierung (Probleme & Anforderungen)
Wenn die Anzahl der installierten Mikrocontroller massiv erhöht wird, verändern sich die Anforderungen an die Infrastruktur drastisch: 

•	Ressourcen- & Netzwerk-Overhead: Die verfügbare Bandbreite und die Verarbeitungskapazität des lokalen Netzwerks werden durch unfiltrierte Datenströme stark beansprucht. 

•	Mass Deployment (Massenbereitstellung): Sicherheitsupdates oder Logikänderungen müssen gleichzeitig auf eine Vielzahl von Geräten ausgerollt werden, ohne jedes Board einzeln per Kabel anzuschließen. 

•	Gewünschte Dienste für die Skalierung: Für den produktiven Betrieb größerer Systeme sind automatisierte Mechanismen zur Überwachung notwendig: 

o	Ein zentrales Logging-System zur Fehlerprotokollierung. 

o	Ein Knoten-Überwachungssystem (Node Monitoring) zur Live-Statuskontrolle. 

o	Simulations- und Stress-Testing-Umgebungen, um Systemgrenzen vor dem echten Deployment zu prüfen. 

3. Gerätemanagement vs. Integration für IoT-Systeme
Um große IoT-Systeme wartbar zu gestalten, muss die Architektur strikt in zwei funktionale Framework-Ebenen unterteilt werden: 

A. Device-Management Frameworks (Geräteverwaltung)

Diese Frameworks agieren direkt auf der Hardware-Ebene und verwalten den gesamten Lebenszyklus der Mikrocontroller (z. B. ESP8266 oder ESP32). 

•	Kernaufgaben: Automatische Firmware-Kompilierung, drahtlose Bereitstellung (Over-the-Air / OTA), physische Pin-Konfiguration und die automatische Anmeldung (Adoption) neuer Geräte im Netzwerk. 

•	Ziel: Aus der nackten Hardware einen einsatzbereiten, netzwerkfähigen IoT-Knoten (Node) zu generieren.

•	Wichtige Vertreter:

o	IoTempower: Maximal optimiert für die Lehre und schnelles Prototyping. Ermöglicht vollständig deklarative Konfigurationen über Verzeichnisstrukturen und ultrakurze setup.cpp-Dateien, bringt ein lokales Offline-Gateway mit und bietet einen sicheren, drahtlosen Adoption-Prozess. 

o	ESPHome: Konfiguration erfolgt komplett ohne C++ Kenntnisse über YAML-Dateien; nahtlose Integration in Home Assistant. 

o	Tasmota: Vorkompilierte Firmware für kommerzielle Smart-Home-Komponenten; Konfiguration erfolgt direkt über ein lokales Web-Interface. 

o	Mongoose OS: Professionelles, kommerzielles Open-Source-Betriebssystem mit Fokus auf JavaScript/C-Programmierung, TLS-Verschlüsselung und native Cloud-Anbindungen. 


B. Integration Frameworks (System-Integration)

Diese Frameworks arbeiten auf der Middleware- und Anwendungsebene. Sie setzen voraus, dass die Hardware bereits funktionsfähig im Netzwerk angemeldet ist. 

•	Kernaufgaben: Logische Verknüpfung und Orchestrierung der Datenströme zwischen den Geräten über Protokolle wie MQTT, Datenkonvertierung und Bereitstellung von grafischen Benutzeroberflächen (Dashboards). 

•	Ziel: Die herstellerunabhängige Kommunikation und die logische Verschaltung aller Komponenten zu einem funktionierenden Gesamtsystem.

•	Wichtige Vertreter:

o	Node-RED: Flussbasierte, visuelle Programmierung mit hoher Flexibilität durch eine riesige Auswahl an Community-Knoten und integrierter Dashboard-Erstellung. 

o	IoTknit: Python-basiertes Framework, das als leichtgewichtige, codebasierte Alternative zu Node-RED dient, um MQTT-Topics direkt via Skript zu orchestrieren. 

o	Home Assistant / OpenHAB: Führende Plattformen im Bereich der Heimautomatisierung mit umfassenden Datenbanken zur Integration kommerzieller Hardware. 

o	Apache NiFi / Flogo: Ausgelegt für industrielle Datenskalierung (Data Routing) und eventgesteuerte Mikro-Architekturen. 
