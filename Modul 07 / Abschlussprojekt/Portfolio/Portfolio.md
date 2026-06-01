## PROTOKOLL-MASTER: 

**Projektname:** Intelligentes Schulwetter- und Sicherheitssystem

**Datum des Treffens:** [TT.MM.JJJJ] | **Ort:** [z. B. Labor / Privat]

**Anwesende Gruppenmitglieder:** Emil, Frederik, Jonathan, Kilian, Minguel, Moritz

**Protokollant:** [Name]

## 1. Zielsetzung des Treffens

•	Zusammenführung der dezentral vorbereiteten ESP32-Knoten im gemeinsamen Netzwerk.

•	Physischer Aufbau des Pappkarton-Schnittmodells (Dirty Prototyping).

•	Testen der gesamten MQTT-Kommunikationskette vom Sensor bis zur Audio-/LED-Aktion.

•	Strukturierung und Zeitplanung für den Dreh des 10-minütigen Abschlussvideos.

## 2. Durchgeführte Arbeiten & Meilensteine

## A. Hardware & Modellbau (Dirty Prototyping)

•	**Status:** [Erfolgreich / Teils erfolgreich]

•	Der Umzugskarton wurde als offenes 3D-Schnittmodell präpariert. Die Zonen (Dach, Klassenraum, Sekretariat) wurden mittels Trennwänden fixiert und beschriftet.

•	**Kabelmanagement:** Es wurden Löcher in die Rückwand gestochen, um die Jumper-Kabel der Sensoren unsichtbar nach hinten zu den Steckbrettern abzuführen.

•	Das 3D-gedruckte Windrad wurde auf dem Dach montiert (Generator-Testbetrieb).

## B. Netzwerk & MQTT-Integration (Die Zusammenführung)

•	**Status:** [Erfolgreich / Teils erfolgreich]


•	Alle 8 ESP32-Boards wurden erfolgreich auf die SSID und das Passwort des gemeinsamen Routers konfiguriert.

•	Der MQTT-Broker auf dem Gateway wurde gestartet, und die Zuordnung der Topics (schulwetter/espX/...) wurde im System validiert.

## C. Funktionstests der einzelnen Knoten

•	**ESP 1 & 2 (Wetterstation):** Live-Test des analogen Regensensors (Auslösung durch Wassertropfen) $\rightarrow$ Daten kommen via MQTT im Node-RED an.

•	**ESP 4 (LED-Warnsystem - Moritz):** Die WS2812B-Zustände schalten bei simuliertem Regen erfolgreich von Grün über Gelb auf Rot.

•	**ESP 5 (Audio - Frederik):** Der DFPlayer empfängt den seriellen UART-Befehl und spielt die MP3-Warnansage laut und verständlich ab.

•	**ESP 7 (RFID - Emil):** Das Einlesen der Karten funktioniert. Die Unterscheidung zwischen gültigem Master-Tag (Freigabe) und ungültigem Tag (Fehlersignal/Summer) läuft stabil.

•	**ESP 6 (Displays - Miguel):** [Status zum aktuellen Stand des OLED/LCD-Einbaus einfügen].

## Nächste Schritte & Offene Aufgaben (Fahrplan)
Bis zum finalen Abgabetermin (Dreh des Videos und Portfolio-Abgabe) wurden folgende Aufgaben verteilt:

## Visueller Nachweis des Treffens

•	[Foto 1: Das Team beim Verkabeln des Pappmodells im Labor]
•	[Foto 2: Screenshot des Node-RED-Fensters, auf dem alle Knoten als 'connected' angezeigt werden]




## Dokumentation

1. Gruppentreff:

   - Wir haben uns in der gruppe getroffen und uns dafür ein Raum in der IMA (benachbartes Gebäude, indem man sich einen Raum mieten kann) gemietet. Im Anschluss haben wir alle Materialien heraus geholt und gesammelt platziert. Durch die vorherige Gruppeneinteilung konnten wir mit den Projektstart direkt beginnen und der MAngo Router konnte eingerichtet werdje, erste Wemos D1 minis wurdne geflashed, Sensoren wurden sich angeschaut und schlau gemacht wie man diese verknüpft und Ideen für die Abschlusspräsentation wurden gesammelt.
  
   - 
