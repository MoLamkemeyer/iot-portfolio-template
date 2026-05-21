# Module 2

We are going to show here notes for Task 1, 2, 3, 4, and 5 to prove


## Task 1

This task was executed by myself.

Was ist ein Stromkreis?
Ein Stromkreis ist ein geschlossenes System, in dem elektrischer Strom fließen kann. Er besteht im Wesentlichen aus:
1.	Einer Spannungsquelle (z. B. einer Batterie oder den 5V/3.3V-Pins eines ESP32), die den Strom „antreibt“.
2.	Einem Verbraucher (z. B. einer LED, einem Widerstand oder einem Motor), der die elektrische Energie nutzt.
3.	Leitern (Kabeln oder Leiterbahnen), die die Komponenten miteinander verbinden.
Damit Strom fließt, muss der Kreis komplett geschlossen sein – vom Pluspol (High/VCC) durch den Verbraucher zurück zum Minuspol (Ground/GND).
Was ist ein Steckbrett für die elektronische Prototypenerstellung?
Ein Steckbrett (oft auch Breadboard genannt) ist das wichtigste Werkzeug, um elektronische Schaltungen schnell und ohne Löten aufzubauen. Du kannst Mikrocontroller, Sensoren, Widerstände und Kabel einfach in die Löcher stecken, um sie miteinander zu verbinden. Da nichts dauerhaft verlötet wird, lässt sich die Schaltung jederzeit blitzschnell verändern, erweitern oder korrigieren.
Beschreibung eines Steckbretts und zwei markante Merkmale
Ein Steckbrett besteht aus einer Kunststoffplatte mit einer Vielzahl von kleinen Einstecklöchern, unter denen sich federnde Metallstreifen befinden. Diese Streifen klemmen die hineingesteckten Bauteile fest und stellen den elektrischen Kontakt her.

Zwei markante Merkmale:
•	Die Bus- oder Stromschienen (Außenbahnen): An den langen Außenseiten verlaufen meist zwei parallele Linien (oft rot für Plus/+ und blau/schwarz für Minus/-). Diese Löcher sind horizontal (längs) über die gesamte Länge miteinander verbunden. Sie dienen dazu, die Stromversorgung für das gesamte Board überall leicht zugänglich zu machen.
•	Die Terminal- oder Steckleisten (Innenbereich): Die Löcher im mittleren Bereich sind in kurzen Spalten angeordnet (oft mit Buchstaben A–E und F–J beschriftet). Diese Spalten sind vertikal (quer) miteinander verbunden. Eine dicke Kerbe in der Mitte des Boards trennt die obere von der unteren Hälfte, sodass man dort integrierte Schaltkreise (ICs) oder Mikrocontroller einstecken kann, ohne deren gegenüberliegende Pins kurzzuschließen.
Konventionen zur Farbcodierung von Kabeln
Um bei einer Schaltung nicht den Überblick zu verlieren, nutzt man weltweit feste Farbkonventionen:
•	Rot: Wird standardmäßig für die positive Spannungsversorgung genutzt (z. B. 5V oder 3.3V).
•	Schwarz (oder Blau): Wird ausnahmslos für die Masse bzw. den Minuspol (GND / Ground) verwendet.
•	Gelb, Grün, Orange etc.: Werden flexibel für Daten- und Signalleitungen eingesetzt (z. B. um einen Sensor auszulesen).
Wie schließt man eine LED an 5V an?
Eine LED darf niemals direkt an eine Spannungsquelle wie 5V angeschlossen werden, da sie sonst sofort durchbrennt. Du musst immer einen Vorwiderstand in Reihe (hintereinander) schalten, um den Strom zu begrenzen.
Schritt-für-Schritt-Aufbau:
1.	Verbinde den 5V-Pin mit dem einen Ende eines Widerstands (z. B. 220 / 330 Ohm)
2.	Verbinde das andere Ende des Widerstands mit der Anode (dem langen Beinchen / Pluspol) der LED.
3.	Verbinde die Kathode (das kurze Beinchen / Minuspol) der LED direkt mit dem GND-Pin (Masse).
Beschreibung einer LED
Eine LED (Light Emitting Diode bzw. Leuchtdiode) ist ein elektronisches Halbleiter-Bauelement, das Licht abgibt, sobald elektrischer Strom in die richtige Richtung durch sie hindurchfließt. Sie ist extrem energieeffizient und langlebig. Sie besitzt zwei ungleich lange Anschlussbeine: Das längere Bein ist die Anode, das kürzere Bein (oft an einer abgeflachten Seite des Kunststoffgehäuses) ist die Kathode .
Was ist das Besondere an Dioden?
Das Besondere an einer Diode (zu denen auch die LED gehört) ist ihre Einbahnstraßen-Funktion. Sie lässt den elektrischen Strom nur in eine einzige Richtung durch (in Durchlassrichtung, von der Anode zur Kathode). Schließt man sie falsch herum an (Sperrrichtung), blockiert sie den Stromfluss komplett wie ein Ventil. Deshalb muss man beim Einbau immer penibel auf die Polung achten.
Eine Sache schien noch immer unklar...
Was unklar ist: Muss der Widerstand zwingend vor der LED (an der Anode) sitzen oder darf er auch nach der LED (zwischen Kathode und GND) platziert werden?
Die Auflösung: Da es sich um einen unverzweigten Stromkreis (eine Reihenschaltung) handelt, ist der Strom an jeder Stelle der Schleife exakt gleich groß. Der Widerstand begrenzt den Gesamtstrom im gesamten Kreis, unabhängig davon, ob er vor oder nach der LED sitzt. Die LED überlebt in beiden Varianten!


## Task 2

This task was executed by my myself. Man findet die Hardware, wenn man auf den folgenden Link drückt. 
It is [here][(https://github.com/partner/iot-portfolio/Module02/Readme.md#task-2)](https://github.com/MoLamkemeyer/iot-portfolio-template/tree/main/Hardware).

## Reflection 2
[Reflection 2](/Reflections/ref02.md)

## Task 3
1. Das Kaffee- & MCU-Rätsel (Video-Inspiration)
Nach dem Anschauen des optionalen Einführungsvideos „Coffee and Computers - The ESP8266“ von Ulno wird die seltsame Verbindung zwischen Kaffee und Mikrocontrollern klar:
•	Die Namensgebung: Eines der ersten einflussreichen Entwicklungsboards auf Basis des ESP8266-Chips hieß „Espresso Lite“ (gefolgt von der Version 2). Es wurde von einem Maker namens William Hieu in Singapur entwickelt. Das Wortspiel mit dem Chiphersteller Espressif liegt hierbei natürlich auf der Hand.
•	Der Preisfaktor: Ulno betont, dass diese leistungsstarken WLAN-Chips so revolutionär sind, weil sie unglaublich günstig sind. Ein einfacher ESP8266-Chip kostet weniger als einen Dollar und ein fertiges Board wie der Wemos D1 Mini oft nicht mehr als der Preis für einen guten Espresso/Kaffee. Dieser extrem niedrige Preis ermöglichte es Studierenden erstmals, sich massenhaft eigene Hardware für Heimprojekte zuzulegen.
2. Technische Vorbereitung: Pinbelegung des Wemos D1 Mini
Bevor Kabel gesteckt werden, muss die Pinbelegung (Pinout) des Wemos D1 Mini analysiert werden. Für dieses Experiment sind primär die Stromversorgungspins wichtig:
•	5V: Liefert die direkte USB-Spannung (Eingang/Ausgang), ideal für die Versorgung der Stromschienen.
•	GND (Ground): Die gemeinsame Masse (Minuspol) für den geschlossenen Stromkreis.
•	Digitale Pins (z. B. D1, D2): Werden später für die Steuerung der LEDs und das Auslesen des Tasters (Buttons) benötigt.
3. Schritt-für-Schritt-Aufbau (Hardware-Prototyping)
Schritt 1: Stromversorgung auf das Steckbrett bringen
1.	Den 5V-Pin des Wemos D1 Mini mit der roten Plus-Schiene (+) des Steckbretts verbinden.
2.	Den GND-Pin des Wemos D1 Mini mit der blauen/schwarzen Minus-Schiene (-) des Steckbretts verbinden. Damit steht die Spannungsversorgung auf dem gesamten Board für alle Bauteile zur Verfügung.
Schritt 2: Verdrahtung der gelben und roten LEDs
1.	Die rote LED mit dem langen Beinchen (Anode) in eine freie Steckreihe setzen.
2.	Einen 330-Ohm-Widerstand nehmen: Ein Ende in dieselbe Reihe wie das lange Bein der LED stecken, das andere Ende mit der roten 5V-Schiene verbinden.
3.	Das kurze Beinchen (Kathode) der roten LED mit einem Kabel an die blaue GND-Schiene anschließen.
4.	Den gleichen Vorgang exakt so für die gelbe LED in einer separaten Steckreihe wiederholen. Ergebnis: Beide LEDs müssen hell leuchten, sobald der Wemos per USB mit Strom versorgt wird.
Schritt 3: Den Taster (Button) hinzufügen
1.	Platziere den Taster so auf dem Steckbrett, dass er die mittlere Trennkerbe überbrückt.
2.	Verbinde eine Seite des Tasters mit der roten 5V-Schiene.
3.	Verbinde die andere Seite des Tasters mit der Anode (dem langen Bein) einer der LEDs (anstelle der direkten Verbindung zur 5V-Schiene).
4.	Test: Drücke den Taster. Schließt sich der Stromkreis, leuchtet die LED auf. Lässt du los, erlischt sie.
4. Dokumentation von Fehltritten & Hürden (Lessons Learned)

•	Fehltritt 1: Wemos D1 mini defekt 
o	Problem: Die erhaltende Wemos D1 mini war defekt. Aufgefallen ist das durch das fehlende Blinken der Wemos D1 mini und durch das Tauschen von voherigen Komponenten (LED, Widerstand, Taster)
o	Lösung: Austausch des defekten Wemos D1 mini. Nach dem neu Erhalt neu verdrahtet und sofort kam es zu Fehler Nummer 2…
•	Fehltritt 2: Wemos D1 mini neu an der falschen Seite mit dem plus Pol und den Ground verbunden 
o	Problem: Der neue Wemos D1 mini wurde an D6 und D7 angeklemmt anstatt an 5V und GND. Es folgte also wieder ein ständiger Austausch der Komponenten mit meinem Partner bis das Problem als Cognitives Problem eingestuft wurde und man merkte das man beim Erhalt des neues Wemos die Anschlussseiten vertauscht hat.
o	Lösung: Tauschen der Pin Belegung auf 5V und GND und sofort hat alles funktioniert. 

<img width="1536" height="2048" alt="Aufgabe3" src="https://github.com/user-attachments/assets/f1a1ffe4-4789-4dd2-925a-0d638a35d876" />

<img width="1536" height="2048" alt="Aufgabe3 1" src="https://github.com/user-attachments/assets/cccfee27-4d06-40a0-8278-d93e676a4961" />

<img width="1536" height="2048" alt="Aufgabe3 2" src="https://github.com/user-attachments/assets/9c0c6d6c-9f98-44a9-be79-c07a00897d77" />

<img width="1536" height="2048" alt="Aufgabe3 3" src="https://github.com/user-attachments/assets/edf254f5-771a-41f7-8c3d-04c8c8d5e298" />


## Task 4
Art der Werkzeuge & Nutzen
Es handelt sich hierbei um EDA-Software (Electronic Design Automation) und Prototyping-/Simulations-Tools. Sie dienen dazu, elektronische Schaltungen digital zu planen, zu visualisieren und zu testen, bevor man sie real aufbaut.
•	Nutzen: * Fehlervermeidung: Schaltungen können virtuell verdrahtet und analysiert werden, um Kurzschlüsse zu verhindern.
o	Dokumentation: Erstellung von sauberen, standardisierten Schaltplänen für Portfolios oder Platinen-Layouts (PCB-Design).
o	Interaktives Lernen: Simulatoren erlauben das Testen von Code direkt mit virtueller Hardware.
Übersicht gängiger Tools: TinkerCAD wurde verwendet!
•	Fritzing: Perfekt für Einsteiger. Es bietet eine realitätsgetreue „Steckbrett-Ansicht“, bei der Bauteile genau so aussehen wie in der Realität.
•	Wokwi / Tinkercad: Cloudbasierte Online-Simulatoren, in denen du einen ESP8266/ESP32 virtuell verdrahten und direkt mit Arduino-Code programmieren kannst.
•	KiCad / EasyEDA: Professionelle Suiten für den echten Schaltplanentwurf und das anschließende Designen von gedruckten Leiterplatten (PCBs).

<img width="843" height="443" alt="aufgabe 4 Taster Arduino" src="https://github.com/user-attachments/assets/2a8ff7cb-eb86-4000-8141-950e1b061479" />
<img width="837" height="445" alt="Aufgabe 4 LED Arduino" src="https://github.com/user-attachments/assets/a4acbc39-1109-4d2f-83d6-75a09f03f40c" />
<img width="926" height="483" alt="Aufgabe 4 LED2 Arduino" src="https://github.com/user-attachments/assets/beaf6d76-836e-4dce-8110-5e26991f2635" />



## Reflection 3
[Reflection 3](/Reflections/ref03.md)


