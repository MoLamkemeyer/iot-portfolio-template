## Abschlussprojekt Reflexion X

## PORTFOLIO-MASTER: Modul 7 – Abschlussprojekt

**Projektname:** Intelligentes Schulwetter- und Sicherheitssystem (Smart School Weather & Safety System)

**Gruppenmitglieder:** Emil, Frederik, Moritz, Jonathan, Minguel

**Eigener Name:** [Dein Name]

**Eigener Schwerpunkt/Knoten:** [z. B. ESP 4 – LED-Warnsystem]

## 1. Architektur & Technische Umsetzung (Mein Beitrag)

**Systemstruktur & Knoten-Setup**

•	Mein zugewiesener Knoten: [z. B. ESP 4 – LED-Warnsystem]

•	Verwendete Sensoren/Aktoren an diesem Knoten: [z. B. WS2812B LED-Streifen, LEDs]

•	Kommunikations-Protokoll: MQTT über das lokale Schul-WLAN.

Mein Programmcode (setup.cpp / Konfiguration)
C++
// [Füge hier deinen exakten C++/IoTempower-Code für deinen Knoten ein]
// Beispiel:
// #define LED_PIN D5
// led(green_led, LED_PIN);
Node-RED-Anbindung & MQTT-Topics
Damit mein Knoten mit der zentralen Steuerung kommuniziert, wurden folgende Datenpunkte definiert:
•	Subscribed Topic (Eingang zum Knoten): schulwetter/[Mein_Knoten]/[Aktor]/set
•	Published Topic (Ausgang vom Knoten): schulwetter/[Mein_Knoten]/[Sensor]

## 2. Die geforderte Projekt-Reflexion**

•	**Wichtigste Erkenntnis (Zusammenfassung):** [Schreibe 1-2 Sätze, was die größte Erkenntnis bei der Kopplung von 8 ESP32-Boards im dezentralen System war.]

•	**Das möchte ich mir merken:** [z. B. Dass man bei komplexen C++ Audio- oder Display-Treibern frühzeitig die Bibliotheken auf Kompatibilität prüfen muss.]

•	**Mein Rat an zukünftige Studierende:** [z. B. Plant die IP- und MQTT-Adressen vor dem Labor fest ein und baut ein Dirty-Prototyping-Modell aus Pappe, um die Hardware-Zonen vorab visuell zu trennen.]

## Was war gut?

•	[z. B. Das Zusammenspiel der automatischen MP3-Sprachdurchsagen mit dem Regensensor-Trigger lief extrem flüssig.]

•	[z. B. Das Dirty-Prototyping mit dem Pappkarton-Schnittmodell hat geholfen, die 8 dezentralen Knoten für die Kamera perfekt sichtbar zu machen.]

## Was war schwierig & wo gab es Hürden?
 
•	**Technische Probleme:** [z. B. Probleme bei der I2C-Adressierung der OLED-Displays oder Aussetzer beim Einlesen der analogen Werte des Windrad-Generators.]

•	**Positive/Unterhaltsame Herausforderungen:** [z. B. Das Experimentieren mit der Pipette auf dem Regensensor oder der mechanische Bau des 3D-Druck-Windrads aus einer alten Motorwelle.]

•	**Verpasste Chancen (Hürden):** [z. B. Bei den Node-RED Server-Verbindungsproblemen hätten wir uns viel früher an den Dozenten oder die Nachbargruppen wenden sollen, statt wertvolle Laborzeit mit der Fehlersuche zu verlieren.]
Interaktion mit Kommilitonen & Dozenten

•	**Kommunikation im Team:** [z. B. Durch die klare Verteilung der 8 ESP-Boards konnte jeder isoliert arbeiten, während die Logik-Zusammenführung gemeinsam am Hauptbildschirm der zentralen Steuerung stattfand.]

•	**Austausch im Kurs:** [z. B. Kurzer Abgleich mit Gruppe X bezüglich der MQTT-Broker-Stabilität unter hoher Netzlast.]

## 3. Hilfe und zusätzliche Arbeit

**Erhaltene Hilfe & Feedback**

•	**Wer hat geholfen:** [z. B. Jonathan hat mir bei der Pin-Zuweisung geholfen / Der Dozent gab Feedback zum Audio-Verstärker.]
•	**Nutzen des Feedbacks:** [z. B. Das Feedback war extrem hilfreich, da wir dadurch das Rauschen auf den Lautsprechern durch einen zusätzlichen Kondensator beheben konnten.]

**Geleistete Hilfe & Feedback**

•	**Wem habe ich geholfen:** [z. B. Ich habe Miguel bei der Fehleranalyse des I2C-Busses für das Display unterstützt.]

•	**Welches Feedback habe ich gegeben:** [z. B. Den Tipp gegeben, die Pull-Up-Widerstände in der Konfiguration zu überprüfen.]
Eigene Sonderleistungen / Kurs-Beiträge

•	**Vorstellungen/Präsentationen:** [z. B. Ich habe den 5-Minuten-Pitch unseres Szenarios vor dem benachbarten Team übernommen.]

•	**Implementierungen & Fixes:** [z. B. Ich habe das Gehäuse für den RFID-Knoten im Pappmodell konstruiert / Einen kritischen Bug im MQTT-Dauersendeschleifen-Skript behoben, der den Broker zum Absturz brachte.]

## 4. Visueller Labor-Nachweis (Anhänge)

•	[Hier Screenshot deines spezifischen Node-RED Logik-Ausschnitts einfügen]

•	[Hier Foto deines verkabelten ESP32-Knotens auf dem Steckbrett einfügen]

•	[Hier Foto des fertigen Pappkarton-Schnittmodells mit den eingebauten Komponenten einfügen]


