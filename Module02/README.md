<img width="900" height="1600" alt="WhatsApp Image 2026-05-21 at 12 59 37" src="https://github.com/user-attachments/assets/42b4d5ba-015c-4405-b3a1-15f66ecc8ba0" />
<img width="900" height="1600" alt="WhatsApp Image 2026-05-21 at 12 59 37" src="https://github.com/user-attachments/assets/d7495b5a-7c55-4807-8617-bd252645d102" />
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
Man findet die zusammenfassende Reflexion in Reflexion 1 in Modul 1


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

## Task 5
1. Portadressierungsschemata
Beim ESP8266/Wemos D1 Mini muss strikt zwischen zwei Nummerierungen unterschieden werden:
•	Board-Pin-Bezeichnung (Siebdruck): Das sind die auf die Platine aufgedruckten Namen (z. B. D0, D1, D4, D6).
•	GPIO-Nummerierung (General Purpose Input Output): Die tatsächliche interne Registernummer des ESP8266-Chips, die vom Prozessor direkt angesprochen wird.
•	Arduino-Abstraktion: Die Arduino-IDE erlaubt es dank der Board-Definitionen, direkt das Alias D6 im Code zu schreiben. Nutzt man andere Frameworks, muss oft die nackte GPIO-Nummer verwendet werden.
2. GPIO- und Board-Pin-Nummer für D6
Anhand des Pinout-Diagramms ergibt sich:
•	Board-Pin: D6
•	Zugehörige interne GPIO-Nummer: GPIO12

<img width="1536" height="2048" alt="Aufgabe6" src="https://github.com/user-attachments/assets/dbb43cc6-e915-4b2a-b559-1da3dee4b391" />

Ab jetzt muss der Nodemcu benutzt werden, da der Wemos D1 mini nicht funktionfähig ist mit dem Blinkprogramm. Nach Besprechung mit dem 2. Tutor ist dies aber auch in Ordnung und das Problem entstehe immer mal wieder auf verschiednen Rechner. Nach dem Versuch den Fehler zu beheben, hat man sich dazu entschlossen von Wemos D1 mini auf Nodemcu zu wechseln. 
<img width="1200" height="1600" alt="Aufgabe 5 blink LED" src="https://github.com/user-attachments/assets/fd5c6891-94b7-4438-9e6f-00bf81a0913a" />

Gleichzeitiges Blinken mit Anschluss D5: (siehe Bild oben)
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
  pinMode(5, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // change state of the LED by setting the pin to the HIGH voltage level
  digitalWrite(5, HIGH); 
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);
  digitalWrite(5, LOW);   // change state of the LED by setting the pin to the LOW voltage level
  delay(1000);                      // wait for a second
}

Abwechselndes Blinken mit Anschluss D5: 
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
  pinMode(5, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // change state of the LED by setting the pin to the HIGH voltage level
  digitalWrite(5, LOW); 
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);
  digitalWrite(5, HIGH);   // change state of the LED by setting the pin to the LOW voltage level
  delay(1000);                      // wait for a second
}

<img width="1536" height="2048" alt="Aufgabe 5 abwechselndes blinken2" src="https://github.com/user-attachments/assets/7b6eb024-9674-4ffc-a454-cb24ee6e35dc" />
<img width="1536" height="2048" alt="Aufgabe 5 abwechselndes blinken1" src="https://github.com/user-attachments/assets/a15d1e63-6e2a-46ac-bd4a-14169214d551" />

Füge eine weitere synchrone LED hinzu auf D2:

<img width="900" height="1600" alt="Aufgabe 5 weitere Led 1" src="https://github.com/user-attachments/assets/2cc5ca5a-db54-455c-a2d7-3505e2a78026" />
<img width="1152" height="2048" alt="Aufgabe 5 weitere LED" src="https://github.com/user-attachments/assets/2ec620b2-dba0-44ec-af4c-cc97626e86de" />


## Task 6

Was ist ein Pull-up-Widerstand?
Ein Pull-up-Widerstand ist ein Widerstand, der eine Signalleitung mit der positiven Versorgungsspannung (hier 3,3 V) verbindet. Er sorgt für einen definierten HIGH-Zustand auf der Leitung, solange der Taster nicht gedrückt ist. Ohne diesen Widerstand würde der Pin im offenen Zustand „schweben“ (Floating Pin) und durch elektromagnetische Störungen unkontrolliert zwischen HIGH und LOW hin- und herspringen.
Lösung über die interne Hardware (INPUT_PULLUP)
Anstatt einen externen Widerstand mühsam auf dem Steckbrett zu verdrahten, nutzt man den im ESP8266 eingebauten Pull-up-Widerstand. Der Taster wird einfach zwischen D3 und GND angeschlossen.

<img width="900" height="1600" alt="WhatsApp Image 2026-05-21 at 12 59 37" src="https://github.com/user-attachments/assets/3ed13395-9142-4f8a-a724-c672a17a1303" />

INPUT_PULLUP:

// digital pin 2 has a pushbutton attached to it. Give it a name:
int pushButton = 4;

// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
  // make the pushbutton's pin an input:
  pinMode(pushButton, INPUT_PULLUP);
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop routine runs over and over again forever:
void loop() {
  if (digitalRead(pushButton))
  {digitalWrite(LED_BUILTIN,HIGH);}
  else
  {digitalWrite(LED_BUILTIN,LOW);} 
  // read the input pin:
  int buttonState = digitalRead(pushButton);
  // print out the state of the button:
  Serial.println(buttonState);
  delay(1);  // delay in between reads for stability
}

<img width="1536" height="2048" alt="Aufgabe 6 PullUp 1" src="https://github.com/user-attachments/assets/c8ce8ac0-fe05-4ced-8597-55bc0f3e8b96" />
<img width="1536" height="2048" alt="Aufgabe 6 PullUp" src="https://github.com/user-attachments/assets/390fa60f-bf03-481b-a23e-2558458d53be" />

Alle Aufgaben wurden im Zusammenarbeit mit meinen Teampartner gemacht ab Aufgabe 7 
<Frederik Bröckling>, [Frederik Bröckling](https://github.com/fbroeckling/Portfolio-of-Frederik-Br-ckling)


## Task 7 Mit Teampartner

1. Das Relaismodul verstehen
•	Was ist ein Relais? Ein elektrisch betätigter Schalter. Mit einem kleinen, isolierten Steuerstrom (3,3 V von der MCU) kann ein mechanischer Kontakt elektromagnetisch umgelegt werden, um einen völlig separaten, großen Laststromkreis (z. B. 12 V für das Magnetschloss oder 230 V) zu schalten.
•	Steuerseite vs. Schaltseite: * Steuerseite: Hat Pins für VCC (Stromversorgung), GND (Masse) und IN (Signal von der MCU). Sie ist galvanisch getrennt.
o	Schaltseite: Besitzt drei Schraubklemmen: COM (Common/Gemeinsamer Kontakt), NO (Normally Open / im Ruhezustand offen) und NC (Normally Closed / im Ruhezustand geschlossen).
•	Standardzustand des Magnetschlosses: Ein Solenoid-Zutrittsschloss benötigt Strom, um den Riegel einzuziehen (Normally-Locked / Ruhestromlos geschlossen). Daher verdrahten wir die externe 12V-Stromversorgung über den NO-Kontakt des Relais.
2. Wichtige Sicherheitswarnung!
WARNUNG: Das Magnetschloss zieht beim Schalten hohe Stromspitzen und erzeugt beim Abschalten eine gefährliche Induktionsspannung. Es darf niemals direkt an die Pins des Wemos angeschlossen werden! Zudem darf die Spule des Schlosses nicht länger als 0,5 Sekunden (500 ms) aktiviert bleiben, da sie sonst überhitzt und durchbrennt!

Funktionsweise des Magnetverriegelungsschlosses 
Ein elektronisches Hubmagnet-Schloss basiert auf dem Prinzip des Elektromagnetismus. Im Inneren des Gehäuses befindet sich eine Spule (Drahtwicklung) und ein beweglicher Eisenkern (der Schließbolzen), der von einer mechanischen Feder nach außen gedrückt wird.
•	Ruhezustand (Stromlos): Die eingebaute Feder drückt den Bolzen nach draußen. Die Tür ist mechanisch verriegelt. 
•	Aktivierter Zustand (Unter Strom): Sobald eine Spannung von 12V an die Spule angelegt wird, fließt Strom. Dieser Strom erzeugt ein starkes magnetisches Feld im Inneren. Die magnetische Kraft zieht den Eisenbolzen entgegen der Federkraft in das Gehäuse hinein. Die Tür ist entriegelt. 
Wichtige Sicherheitswarnung aus dem Labor!
ACHTUNG (Zerstörungsgefahr): Die Magnetspule ist für den Kurzzeitbetrieb ausgelegt. Wird die Spule länger als 0,5 Sekunden (500 ms) dauerhaft mit Strom versorgt, erhitzte sie sich extrem stark, die Isolierung des Drahtes schmilzt und das Schloss brennt durch! Im Code muss das Ausschalten zwingend über ein kurzes delay(500) sichergestellt werden. 
2. Die Standardzustände im Systemkontext
Beim Aufbau eines Zutrittskontrollsystems (z. B. an der Erste-Hilfe-Station) müssen wir die Begriffe für die Standardzustände der Hardware exakt trennen:
•	Schloss-Zustand: Normally-Locked (Ruhestromlos geschlossen): Das Schloss ist im unbestromten Zustand zu. Fällt der Strom im Gebäude aus, bleibt das Schloss verriegelt. 
•	Relais-Anschluss: Normally-Open (NO / Arbeitskontakt): Das Relais schaltet die externe 12V-Leitung zum Schloss erst dann durch, wenn es vom Mikrocontroller den aktiven Befehl dazu erhält. 
•	Relais-Ansteuerung: Active-Low: Die Steuerplatine des Relais zieht an, wenn der Wemos-Pin auf LOW (0V) gezogen wird.

<img width="1536" height="2048" alt="Aufgabe 7" src="https://github.com/user-attachments/assets/08659746-f2b4-4a9c-aad5-2e144f3adfa3" />

Der passende Code zum Bild
void setup() {
  // put your setup code here, to run once:
  pinMode(D6, INPUT);
  pinMode(D7, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(D7, HIGH);
  delay(400);
  digitalWrite(D7, LOW);
  delay(2000);
}

Mit Taster: 

<img width="1536" height="2048" alt="Aufgabe 7 mit taster" src="https://github.com/user-attachments/assets/174b9260-f9e9-4443-a569-5e8a92879ff5" />

void setup() {
  // put your setup code here, to run once:
  pinMode(D6, INPUT_PULLUP);
  pinMode(D7, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  if (digitalRead(D6))
  {
    digitalWrite(D7, LOW);
  }
  else
  {
    digitalWrite(D7, HIGH);
  }
}

## Task 8 Mit Teampartner

Was ist PWM?
PWM steht für Pulsweitenmodulation. Da ein Mikrocontroller-Pin rein digital nur HIGH (3,3 V) oder LOW (0 V) ausgeben kann, simuliert man eine analoge Spannung durch extrem schnelles Umschalten zwischen diesen beiden Zuständen. Das Verhältnis zwischen der Einschaltzeit zur Gesamtaufzeit nennt man Tastgrad (Duty Cycle). Je länger der Pin auf HIGH steht, desto heller leuchtet die LED.


<img width="1536" height="2048" alt="Aufgabe8" src="https://github.com/user-attachments/assets/5ec62ce7-58c8-4abf-8db0-81e420107f2c" />
<img width="1536" height="2048" alt="Aufgabe 8" src="https://github.com/user-attachments/assets/a50bc833-5517-4b53-9e8a-079898050cf1" />

void setup() {
  // put your setup code here, to run once:
  pinMode(D6, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  for (int i = 0; i <= 255; i++)
  {
    analogWrite(D6, i);
    delay(10);
  }
  delay(2000);
  for (int i = 255; i >= 0; i--)
  {
    analogWrite(D6, i);
    delay(10);
  }
  delay(2000);
}

## Task 9 Mit Teampartner

Bus-Systeme & Peripheriekommunikation (Kurzübersicht für dein Portfolio)
•	GPIO / PWM: Allgemeine digitale Ein-/Ausgangspins für einfache Schaltsignale (Taster, Relais) oder zeitkritische Pulsmodulationen (Dimmen, Servos).

•	I2C (Inter-Integrated Circuit): Ein synchroner, halbduplexer 2-Draht-Bus (SDA für Daten, SCL für den Takt). Er ist master-slave-basiert und erlaubt es, dutzende Sensoren (z. B. Displays, Barometer) parallel über dieselben zwei Leitungen anzusprechen.

•	SPI (Serial Peripheral Interface): Ein sehr schneller, synchroner 4-Draht-Bus (MOSI, MISO, SCK, CS). Ideal für datenintensive Anwendungen wie SD-Kartenleser oder TFT-Displays.

•	UART (Universal Asynchronous Receiver-Transmitter): Eine asynchrone Punkt-zu-Punkt-Verbindung über zwei Leitungen (TX und RX). Wird standardmäßig für die serielle Kommunikation mit dem PC (USB-Schnittstelle) genutzt. RS232/RS485 sind industrielle Pegel-Erweiterungen davon.

•	OneWire (Eindraht-Bus): Ein von Dallas Semiconductor entwickelter Bus, der neben Masse nur eine einzige Datenleitung benötigt (z. B. für den Temperatursensor DS18B20).

Achtung (Das Spiegelbild): Achte beim Stecken der Komponenten auf dem Breadboard immer darauf, ob du die Pins von oben (Top View) oder von unten (Bottom View auf die Lötpunkte) betrachtet hast. Verwechselt man die Seiten, spiegelt man versehentlich die Spannungsversorgung (VCC und GND), was die Bauteile sofort zerstören kann!

UART siehe Aufgabe 7
GPIO / PWM siehe Aufgabe 5 und 8


## Reflection 3
[Reflection 3](/Reflections/ref03.md)
siehe Reflexion 1 in Modul 1: Es ist eine zusammenfassende Reflexion des gesamten ersten Tages des Blockkurs.

