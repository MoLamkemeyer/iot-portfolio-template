## Portfolio-Reflexion: Module 6 & 7 (Systemintegration & Projekt-Kick-off)

**1. Was war gut? (Erfolgreiche Vernetzung in Modul 6)**
- Funktionierende IoT-Kette: Das Zusammenspiel über IoTempower hat heute super geklappt, sodass wir am Ende 3 bis 4 Knoten erfolgreich über ein einziges, zentrales Node-RED-System steuern konnten.
- Klare Rollenverteilung: Unsere Gruppenaufteilung im Labor hat sich schnell eingespielt:
Emil übernahm den RFID-Sensor,
Frederik den Summer,
Minguel das OLED-Display
und ich die Steuerung der LEDs(Diese wurden Hardwaretechnisch schnell und einfach verdrahtet und das Programm auf dem Wemos gespielt).

- Erfolgreiches Testszenario: Das logische Zusammenspiel an der Rezeption lief flüssig. Karte vor den RFID-Sensor halten $\rightarrow$ Node-RED prüft die ID $\rightarrow$ bei "Zutritt gewährt" leuchtet meine grüne Lönt ein tiefer, unmissverständlicher Abweisungston. Die Anzeige des OLED-Display zeigt Zutritt Denied.
  
- Agiler Fokus: Es war stark zu sehen, wie schnell sich die Datenpakete via MQTT im lokalen Netzwerk ohne spürbare Latenz verteilen, sobald die setup.cpp einmal auf den Wemos-Boards läuft.

**Was war schwierig & wo gab es Hürden?**

Node-RED Server-Sperre: Der Aufruf und Start von Node-RED war auf meinem Ubuntu-System schlichtweg nicht realisierbar und hat gestreikt.

**Ausblick auf Modul 7 (Das Abschlussprojekt)**

**Szenario-Entwicklung:** Wir haben die Laborzeit direkt genutzt, um uns im Team intensive Gedanken über die Geschichte und das finale Szenario für unser Abschlussprojekt zu machen.

**Strukturierte Vorbereitung:** Wir haben die komplette Hardware-Liste inklusive aller benötigten Sensoren und Aktoren final definiert und eine feste Aufgabenverteilung erstellt (wer welchen Knoten baut und programmiert).

**Mechatronischer Fahrplan:** Um nicht wieder in Zeitnot zu geraten, haben wir bereits den nächsten festen Termin für ein gemeinsames Treffen vereinbart. Bis dahin arbeitet jeder seine Knoten im Home-Office isoliert vor (Schreiben der setup.cpp und Vorbereitung des Dashboards), damit wir beim Treffen alle Komponenten nur noch zentral über den Mango-Router miteinander verbinden müssen.

**4. Wichtigste Erkenntnis & Rat für die Zukunft**

**Wichtigste Erkenntnis:** Ein IoT-System steht und fällt mit der Flexibilität des Teams. Wenn die Software auf einem Laptop streikt, darf das Projekt nicht stehenbleiben – durch die modulare Aufteilung der Knoten konnten wir das Problem perfekt kompensieren.

**Mein Rat an andere:** Testet die Integration einzelner, komplexer Komponenten (wie das OLED) ganz früh im Prozess. Nutzt die Zeit vor dem nächsten Meilenstein für die isolierte Vorarbeit, damit das finale Zusammenstecken im Labor nicht im Chaos endet.
